# MVP Scope

The MVP should prove that personal go-links are useful outside an enterprise
workspace and that Enbox can power a real consumer-facing app.

## MVP Goal

Let one user create, resolve, edit, import, export, and sync a personal route
namespace across at least one browser using Enbox as the core data layer.

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

### Route Resolution

Users can type a route in a supported entry point and land on the destination.

Initial acceptable entry points:

- browser extension keyword, such as `nav budget`
- hosted resolver, such as `https://navastra.app/go/budget`
- local development resolver for testing

### Enbox Persistence

Routes are stored as Enbox records from v0.

The MVP should exercise:

- `@enbox/api` or `@enbox/browser` connection flow
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

1. Install the extension or open the web app.
2. Create the first route.
3. Store it as an Enbox record.
4. Resolve the route from the browser.
5. Import bookmarks.
6. Promote selected bookmarks into memorable route names.
7. Export routes to prove portability.

## Non-Goals

- Do not build a general-purpose bookmark replacement first.
- Do not require users to understand identity infrastructure.
- Do not make sharing required for the core product to be useful.
- Do not optimize for enterprise administration in v0.
- Do not hide Enbox from the architecture; this is a reference app.

## Validation Questions

- Do people create route names naturally?
- Does address-bar resolution become a daily habit?
- Which syntax feels best: `nav foo`, `go/foo`, `n/foo`, or hosted URLs?
- Do people prefer manual naming, bookmark import, or suggestions?
- Which Enbox APIs feel great in a real app, and which need smoothing?
