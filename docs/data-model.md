# Data Model

The data model should be small, explicit, portable, and represented as an Enbox
protocol from v0.

## Route

A route maps a memorable name to a destination.

```json
{
  "id": "route_01JZ0000000000000000000000",
  "name": "budget",
  "destination": {
    "type": "url",
    "url": "https://example.com/spreadsheets/household-budget"
  },
  "title": "Household Budget",
  "description": "Main budget spreadsheet",
  "tags": ["finance", "home"],
  "collectionIds": ["collection_personal"],
  "createdAt": "2026-07-07T00:00:00.000Z",
  "updatedAt": "2026-07-07T00:00:00.000Z"
}
```

## Route Fields

- `id`: stable unique identifier
- `name`: user-facing alias
- `destination`: target action, initially URL-only
- `title`: readable display name
- `description`: optional note
- `tags`: optional labels for search and organization
- `collectionIds`: optional grouping
- `createdAt`: creation timestamp
- `updatedAt`: last update timestamp

## Name Rules

Initial route names should:

- use lowercase letters, numbers, dashes, underscores, and slashes
- be case-insensitive at resolution time
- trim leading and trailing slashes
- reject empty segments
- avoid whitespace

Examples:

```text
budget
docs/api
github/navastra
home/router
work/payroll
```

## Destination Types

V0 should only require URL destinations.

Future destination types may include:

- search templates
- local files
- app deep links
- mailto links
- command actions
- collection landing pages

## Collection

A collection groups routes for import, export, sharing, or display.

```json
{
  "id": "collection_personal",
  "name": "personal",
  "title": "Personal",
  "description": "Default personal namespace",
  "visibility": "private",
  "createdAt": "2026-07-07T00:00:00.000Z",
  "updatedAt": "2026-07-07T00:00:00.000Z"
}
```

## Usage Event

Usage should be local by default. If remote analytics are ever added, they
should be opt-in.

```json
{
  "routeId": "route_01JZ0000000000000000000000",
  "resolvedAt": "2026-07-07T00:00:00.000Z",
  "source": "extension"
}
```

## Export Format

The export format should be plain JSON:

```json
{
  "schema": "navastra.routes.v1",
  "exportedAt": "2026-07-07T00:00:00.000Z",
  "routes": [],
  "collections": []
}
```

## Sync Notes

The route schema should be storage-neutral in shape, but Enbox is the canonical
runtime. Exports, tests, and future tooling should read and write the same
logical data that is stored in Enbox records.

## Enbox Protocol Sketch

The first implementation should define a Navastra protocol with route and
collection record types.

```ts
import { defineProtocol } from '@enbox/browser';

export const NavastraProtocol = defineProtocol({
  protocol: 'https://navastra.app/protocols/routes',
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
    collection: {},
  },
} as const, {} as {
  route: Route;
  collection: Collection;
});
```

Route names should be available as tags so clients can query and hydrate local
caches efficiently. The encrypted record body remains the source of truth.

## Route Cache Shape

The resolver cache should be derived data, not a second source of truth.

```ts
type RouteCacheEntry = {
  name: string;
  routeId: string;
  url: string;
  title?: string;
  updatedAt: string;
};
```

Cache updates should happen after:

- initial Enbox route query
- route create/update/delete
- live query events from `records.subscribe()` when available
- explicit resync or session restore

The cache can live in extension storage or IndexedDB depending on the client,
but it must be rebuildable from Enbox records.
