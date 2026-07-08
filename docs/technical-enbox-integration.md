# Technical Enbox Integration

This document maps Navastra's first implementation to the current Enbox SDK
shape.

Enbox is in research preview, so this should be treated as a living integration
plan. The direction is still clear: Navastra should use Enbox as the app's
primary identity, storage, and sync layer from v0.

## Packages

For browser-facing app code, start with `@enbox/browser`:

```bash
bun add @enbox/browser
```

`@enbox/browser` re-exports the high-level app APIs from `@enbox/api`, auth and
session helpers from `@enbox/auth`, and browser connect utilities such as
`BrowserConnectHandler`.

Use `@enbox/api` directly only for shared non-browser code where the browser
helpers are not needed.

## Runtime Shape

Navastra should follow Enbox's normal SDK stack:

```text
Navastra web app / extension
  -> @enbox/browser
    -> @enbox/api
      -> @enbox/auth
        -> @enbox/agent
          -> local DWN + remote DWN sync
```

The product-level local route cache is separate from Enbox's own browser
storage. Enbox's browser agent storage is Level-backed through IndexedDB and
coordinates across tabs, workers, and service workers. Navastra should not swap
that storage for an in-memory store.

## Protocol Definition

Create a single route protocol first. Keep it owner-private in v0.

```ts
import { defineProtocol } from '@enbox/browser';

export type RouteData = {
  name: string;
  destination: {
    type: 'url';
    url: string;
  };
  title?: string;
  description?: string;
  tags?: string[];
  collectionIds?: string[];
  createdAt: string;
  updatedAt: string;
};

export type CollectionData = {
  name: string;
  title: string;
  description?: string;
  visibility: 'private' | 'published';
  createdAt: string;
  updatedAt: string;
};

export const NAVASTRA_PROTOCOL_URI = 'https://navastra.app/protocols/routes';

export const NavastraProtocol = defineProtocol({
  protocol: NAVASTRA_PROTOCOL_URI,
  published: false,
  types: {
    route: {
      schema: 'https://navastra.app/schemas/route',
      dataFormats: ['application/json'],
      encryptionRequired: true,
    },
    collection: {
      schema: 'https://navastra.app/schemas/collection',
      dataFormats: ['application/json'],
      encryptionRequired: true,
    },
  },
  structure: {
    route: {
      $tags: {
        name: { type: 'string' },
        collection: { type: 'string' },
      },
    },
    collection: {
      $tags: {
        name: { type: 'string' },
      },
    },
  },
} as const, {} as {
  route: RouteData;
  collection: CollectionData;
});
```

Use encrypted records because route destinations can reveal private work,
financial, medical, home, or social context.

## Connect Flow

For the first browser build:

```ts
import { BrowserConnectHandler, Enbox } from '@enbox/browser';
import { NavastraProtocol, NAVASTRA_PROTOCOL_URI } from './navastra-protocol';

export async function connectNavastra(userPassword: string) {
  return Enbox.connect({
    password: userPassword,
    createIdentity: true,
    dwnEndpoints: ['https://enbox-dwn.fly.dev'],
    identitySyncProtocols: [NAVASTRA_PROTOCOL_URI],
    protocols: [NavastraProtocol],
    connectHandler: BrowserConnectHandler({ appName: 'Navastra' }),
    registration: {
      persistTokens: true,
      onSuccess: () => {},
      onFailure: (error) => console.error(error),
    },
  });
}
```

Notes:

- `Enbox.connect()` returns `{ auth, enbox, session }`.
- `session.did` is the active identity DID.
- `session.recoveryPhrase` may be present on first run and should be shown to
  the user once.
- `identitySyncProtocols` should scope sync to the Navastra protocol.
- Omit `sync` for live WebSocket sync where available, use an interval like
  `'30s'` for polling, or `'off'` only for explicit offline/dev modes.

## Route CRUD

Use the typed protocol API:

```ts
const routes = enbox.using(NavastraProtocol);

export async function createRoute(input: RouteData) {
  return routes.records.create('route', {
    data: input,
    tags: {
      name: input.name,
      collection: input.collectionIds?.[0] ?? 'personal',
    },
  });
}

export async function listRoutes() {
  return routes.records.query('route', {
    dateSort: 'createdDescending',
    pagination: { limit: 100 },
  });
}

export async function readRoute(recordId: string) {
  return routes.records.read('route', {
    filter: { recordId },
  });
}
```

Returned records expose typed `record.data.json()`.

For updates, use the record instance returned by read or query:

```ts
const { record } = await readRoute(routeId);
if (record === undefined) throw new Error('Route not found');

await record.update({
  data: {
    ...await record.data.json(),
    destination: { type: 'url', url: nextUrl },
    updatedAt: new Date().toISOString(),
  },
});
```

For deletion:

```ts
await record.delete();
```

## Live Route Updates

If subscriptions are stable enough for the first build, use them to keep the
route manager and resolver cache current:

```ts
const { liveQuery } = await routes.records.subscribe('route');

for (const record of liveQuery.records) {
  await upsertCacheEntry(record);
}

liveQuery.on('create', upsertCacheEntry);
liveQuery.on('update', upsertCacheEntry);
liveQuery.on('delete', removeCacheEntry);
```

Close live queries when the app or view is disposed:

```ts
await liveQuery.close();
```

## Resolver Cache

The browser extension should resolve from a compact cache:

```ts
type RouteCacheEntry = {
  name: string;
  routeId: string;
  url: string;
  title?: string;
  updatedAt: string;
};
```

Hydrate that cache from Enbox records:

1. Connect or restore session.
2. Query `route` records.
3. Read `record.data.json()`.
4. Normalize route names.
5. Store cache entries for extension lookup.
6. Subscribe to updates when available.

Enbox remains the source of truth. The cache exists only to make address-bar
resolution instant.

## Development DWN

Use one of these during development:

- Enbox preview DWN: `https://enbox-dwn.fly.dev`
- Local DWN server from the Enbox repo

Local server option:

```bash
cd /path/to/enbox/packages/dwn-server
docker compose up -d
```

The default local server URL is:

```text
http://localhost:3000
```

## Implementation Risks

- Enbox APIs may change while it is in research preview.
- Browser extension service workers may need careful bundling with
  `@enbox/browser`.
- The extension may not be able to hold the full Enbox session lifecycle in all
  browsers; the web app can own the session and publish a resolver cache to
  extension storage if needed.
- Encrypted route data is correct for privacy, but route-name tags may still be
  metadata. Treat route names as potentially sensitive in shared or published
  scenarios.
- Sync should be scoped to the Navastra protocol to avoid surprising users or
  pulling unrelated DWN data.
