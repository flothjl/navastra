# MVP Scope

The MVP should prove that personal go-links are useful outside an enterprise
workspace.

## MVP Goal

Let one user create, resolve, edit, import, and export a personal route
namespace across at least one browser.

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
- decentralized storage beyond a simple adapter boundary

## MVP User Flow

1. Install the extension or open the web app.
2. Create the first route.
3. Resolve the route from the browser.
4. Import bookmarks.
5. Promote selected bookmarks into memorable route names.
6. Export routes to prove portability.

## Non-Goals

- Do not build a general-purpose bookmark replacement first.
- Do not require users to understand identity infrastructure.
- Do not make sharing required for the core product to be useful.
- Do not optimize for enterprise administration in v0.

## Validation Questions

- Do people create route names naturally?
- Does address-bar resolution become a daily habit?
- Which syntax feels best: `nav foo`, `go/foo`, `n/foo`, or hosted URLs?
- Do people prefer manual naming, bookmark import, or suggestions?
- Is portability a meaningful reason to choose Navastra, or only a retention
  feature after the product is useful?
