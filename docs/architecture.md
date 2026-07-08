# Architecture

Navastra should be built as an Enbox-first app with a small set of clear client
layers:

```text
Browser / Web UI
      |
Route Resolver
      |
Local Route Cache
      |
Enbox Route Store
      |
User DID + DWN Sync
```

## Design Principles

- **Resolution should be fast:** route lookup must feel instant.
- **Storage should be Enbox-native:** route data should be stored as typed
  Enbox records from the first build.
- **Sync should prove the platform:** the app should exercise Enbox auth,
  record CRUD, subscriptions, session restore, and DWN sync.
- **Identity should be useful, not loud:** users should benefit from ownership
  without needing to learn new terminology on day one.
- **Offline should degrade gracefully:** cached routes should continue to work.

## Components

### Browser Extension

The extension is the most important client because address-bar behavior is the
core product loop.

Responsibilities:

- capture route syntax from the omnibox
- resolve route names from local cache
- redirect to destinations
- open route management UI
- hydrate and update the local route cache from Enbox records

### Web App

The web app manages routes and settings.

Responsibilities:

- create and edit routes
- search and filter routes
- import and export route data
- manage collections
- connect to Enbox
- show sync and session state

### Resolver

The resolver converts route names into destinations.

Responsibilities:

- normalize route names
- search exact aliases first
- support scoped names like `work/payroll`
- return a redirect target or a not-found state
- record optional local usage metadata

### Local Cache

The local cache keeps route lookup fast and resilient.

Possible storage options:

- IndexedDB for browser clients
- SQLite for a future desktop/native client
- in-memory cache for server-side resolver requests

### Enbox Route Store

The Enbox route store is the primary persistence layer.

Responsibilities:

- define the Navastra route protocol
- create, query, update, and delete route records
- restore sessions
- subscribe to route changes where useful
- sync against a development or self-hosted DWN endpoint

The route schema should remain portable and versioned, but Enbox is not a
pluggable afterthought. Navastra should be a serious demonstration of the Enbox
application model.

### User DID And DWN Sync

Long term, users should be able to keep their route namespace in storage they
control. Enbox gives Navastra that foundation through DIDs, typed protocols,
encrypted records, local vaults, and DWN sync.

## Address-Bar Resolution Options

### Extension Keyword

Example:

```text
nav budget
```

Pros:

- reliable in modern browsers
- no DNS setup
- fast for MVP

Cons:

- browser-specific installation
- not exactly `go/foo`

### Hosted Resolver

Example:

```text
https://navastra.app/go/budget
```

Pros:

- works anywhere
- easy to share
- good fallback

Cons:

- less magical
- requires hosted service

### Custom Search Engine

Example:

```text
n budget
```

Pros:

- works without extension in some browsers
- lightweight

Cons:

- setup friction
- inconsistent browser support

### Local Resolver

Example:

```text
http://nav/budget
```

Pros:

- powerful for technical users
- can support OS-level workflows

Cons:

- too much setup for normal consumers
- platform-specific

## Recommended V0 Path

1. Browser extension keyword resolution.
2. Web app for route management.
3. IndexedDB cache.
4. Enbox protocol for routes.
5. Route CRUD through Enbox records.
6. Session restore and sync against a development DWN endpoint.
7. JSON import/export as a portability and debugging feature.
8. Hosted resolver as a convenience layer, not the source of truth.
