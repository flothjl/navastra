# User Experience

Navastra should feel like a tool people can adopt in minutes and keep using for
years.

## Product Feel

- fast
- quiet
- precise
- personal
- trustworthy
- slightly futuristic

The product should not feel like enterprise IT software or a generic bookmark
manager.

## First-Run Experience

The first session should get a user to one successful jump quickly:

1. Install or open Navastra.
2. Connect or create an Enbox-backed identity with minimal friction.
3. Add a first route.
4. Store the route through Enbox.
5. Try the route from the address bar.
6. Land on the destination.
7. See a small route list with edit and import options.

## Address-Bar Syntax

The syntax should be short and easy to remember.

MVP syntax:

```text
nav budget
nav docs/api
nav github/navastra
```

This uses the browser extension omnibox keyword flow. The user types `nav`,
activates the extension keyword, then types the route name.

Future or fallback syntax candidates:

```text
n budget
go budget
nav/budget
```

A hosted resolver can support URLs like:

```text
https://navastra.app/go/budget
```

The hosted resolver should be a fallback and sharing surface, not the first
habit to validate.

## Route Manager

The route manager should prioritize scanning and editing.

Important views:

- all routes
- recently used
- recently created
- broken or unchecked links
- collections
- import review

Important actions:

- create route
- edit destination
- copy route
- duplicate route
- delete route
- export routes
- import bookmarks

## Import Experience

Browser bookmarks are messy. Import should not dump everything into the main
namespace.

Recommended import flow:

1. Upload bookmark export.
2. Show folders and candidate links.
3. Suggest route names.
4. Let the user promote selected bookmarks into active routes.
5. Keep the rest in an imported collection or discard them.

## Not-Found Experience

When a route is missing, Navastra should help the user recover.

Options:

- show nearest matches
- offer to create the route
- search imported bookmarks
- search recent browser history if permission exists

Example:

```text
No route named "payrol".
Did you mean "payroll"?
```

## Sharing Experience

Sharing should feel scoped and intentional.

Examples:

- share a single route
- export a collection
- publish a read-only collection
- subscribe to someone else's public collection

The default state should be private.

## Tone

Use plain language:

- route
- name
- destination
- collection
- import
- export
- sync

Avoid leading with technical language:

- DID
- DWN
- decentralized
- self-sovereign
- cryptographic identity

Those concepts can appear in advanced settings, developer docs, and architecture
notes.

## Enbox Visibility

Users should see simple product language first:

- sync
- portable routes
- private by default
- your namespace

Developers should be able to find Enbox details quickly:

- active DID
- DWN endpoint
- protocol version
- record count
- sync status
- export/debug tools
