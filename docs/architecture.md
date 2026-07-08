# Architecture

Navastra should be built as a small set of replaceable layers:

```text
Browser / Web UI
      |
Route Resolver
      |
Local Route Cache
      |
Sync Adapter
      |
User-Controlled Storage
```

## Design Principles

- **Resolution should be fast:** route lookup must feel instant.
- **Storage should be portable:** route data should use a documented schema.
- **Sync should be replaceable:** the app should not depend permanently on one
  backend.
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
- sync route cache in the background

### Web App

The web app manages routes and settings.

Responsibilities:

- create and edit routes
- search and filter routes
- import and export route data
- manage collections
- configure sync provider

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

### Sync Adapter

The sync adapter abstracts remote persistence.

Initial adapter options:

- simple hosted API for fast MVP
- file-backed sync for local development
- Decentralized Web Node adapter using Enbox or similar tooling

The public route schema should remain stable regardless of adapter choice.

### Storage Layer

Long term, users should be able to keep their route namespace in storage they
control. A DWN-backed implementation is a strong candidate because it gives the
product portable identity and data ownership without making that the main user
story.

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
4. JSON import/export.
5. Sync adapter interface.
6. Hosted API or file-backed adapter for first build.
7. DWN/Enbox adapter exploration after the core loop feels good.
