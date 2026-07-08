# Navastra

Navastra is a personal navigation layer for the web.

It turns short, memorable names into destinations so people can get back to the
apps, docs, dashboards, repos, and references they use every day without hunting
through bookmarks, tabs, chats, or search history.

The starting point is simple:

```text
nav/mail
nav/budget
nav/docs/api
nav/josh/calendar
```

Under the hood, Navastra is designed to be portable, local-first, and identity
aware. A user's namespace should belong to them, sync across devices, and remain
usable without being trapped inside a single workspace or browser account.

## Why

Bookmarks are too passive. Search is too broad. Browser history is noisy.
Enterprise go-link tools are useful, but they usually assume a company-owned
namespace.

Navastra is for personal and small-group link recall:

- Give important destinations human names.
- Resolve those names instantly from the address bar.
- Sync a namespace across devices.
- Share selected aliases with trusted people.
- Keep the underlying data portable.

## Product Pillars

- **Fast recall:** a short name should beat searching, clicking, or asking.
- **Personal namespace:** names should reflect how the user thinks.
- **Portable by design:** the user's aliases should not be locked to one vendor.
- **Local-first feel:** common routes should resolve quickly and work from cache.
- **Shareable when useful:** people should be able to publish or subscribe to
  small sets of routes without giving up control of their full namespace.

## Docs

- [Product Brief](docs/product-brief.md)
- [MVP Scope](docs/mvp.md)
- [Architecture](docs/architecture.md)
- [Data Model](docs/data-model.md)
- [User Experience](docs/user-experience.md)
- [Roadmap](docs/roadmap.md)
- [Open Questions](docs/open-questions.md)

## Status

This repository is in v0 documentation mode. The next milestone is to validate
the core address-bar workflow and choose the first technical path for namespace
storage and sync.
