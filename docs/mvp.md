# MVP Scope

The MVP should prove that personal go-links are useful outside an enterprise
workspace and that Enbox can power a real consumer-facing app.

## MVP Goal

Let one user install a browser extension, create routes, resolve them from the
omnibox, edit/import/export them from a route manager, and sync the namespace
with Enbox as the core data layer.

## Core Concepts

- **Route:** a short name that resolves to a destination.
- **Namespace:** a user's collection of route names.
- **Destination:** the URL or action a route points to.
- **Collection:** a named subset of routes that can be exported, imported, or
  shared later.

## Required Features

### Route Creation

Users can create a route with:

- name
- URL
- optional title
- optional description
- optional tags

Example:

```text
name: budget
url: https://example.com/spreadsheets/household-budget
```

### Extension-First Route Resolution

Users can type a route in a supported entry point and land on the destination.

The MVP entry point is a browser extension omnibox keyword:

```text
nav budget
nav github/navastra
nav docs/api
```

The extension should:

- register an omnibox keyword
- normalize the route query
- resolve from a compact local cache
- redirect immediately on exact match
- show suggestions or a not-found page when no route matches

A hosted resolver like `https://navastra.app/go/budget` can exist as a fallback
and sharing surface, but it is not the primary MVP loop.

### Enbox Persistence

Routes are stored as Enbox records from v0.

The MVP should exercise:

- `@enbox/browser` connection flow
- typed protocol definition for routes
- record create, query, update, and delete
- session restore
- local cache hydrated from Enbox records
- sync against a development DWN endpoint

### Route Management

Users can:

- list routes
- search routes
- update a destination
- rename a route
- delete a route
- copy a resolver URL

### Import And Export

Users can:

- import a browser bookmarks HTML file
- export routes as JSON
- export routes as Markdown

### Local Cache

The client should keep a local cache of routes so common jumps feel instant and
can survive temporary sync failure.

## Deferred Features

These are important, but not required for the first validation build:

- multi-user accounts
- paid plans
- team administration
- analytics dashboards
- native mobile apps
- granular permissions
- browser history intelligence
- AI route suggestions
- encrypted shared collections
- non-Enbox persistence as a first-class path

## MVP User Flow

1. Install the extension.
2. Connect or create an Enbox-backed identity.
3. Create the first route in the route manager.
4. Store it as an Enbox record.
5. Hydrate the extension resolver cache.
6. Type `nav budget` in the omnibox.
7. Resolve the route from the browser.
8. Import bookmarks.
9. Promote selected bookmarks into memorable route names.
10. Export routes to prove portability.

## Non-Goals

- Do not build a general-purpose bookmark replacement first.
- Do not require users to understand identity infrastructure.
- Do not make sharing required for the core product to be useful.
- Do not optimize for enterprise administration in v0.
- Do not hide Enbox from the architecture; this is a reference app.
- Do not make the hosted resolver the primary MVP path.

## Validation Questions

- Do people create route names naturally?
- Does omnibox resolution become a daily habit?
- Which syntax feels best: `nav foo`, `go/foo`, `n/foo`, or hosted URLs?
- Do people prefer manual naming, bookmark import, or suggestions?
- Which Enbox APIs feel great in a real app, and which need smoothing?
