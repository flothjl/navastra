# Roadmap

## Phase 0: Documentation And Decisions

- define product brief
- define MVP scope
- define route schema
- decide first address-bar workflow
- choose first client stack
- define Enbox route protocol
- choose development DWN endpoint

## Phase 1: Local Prototype

- web app route manager
- Enbox connect/session restore
- Enbox-backed route store
- create, edit, delete, search routes through Enbox records
- JSON import/export
- hosted-style resolver route in development
- manual testing with seed routes

## Phase 2: Browser Extension

- extension keyword support
- local cache
- redirect flow
- not-found page
- route creation shortcut from current tab
- cache hydration from Enbox records

## Phase 3: Import And Portability

- browser bookmark import
- import review screen
- route name suggestions
- Markdown export
- route schema versioning
- backup and restore

## Phase 4: Enbox Sync

- development DWN sync
- conflict handling rules
- local cache invalidation
- multi-device smoke testing
- subscription-driven route manager updates

## Phase 5: Ownership Layer Polish

- define identity and authorization model
- support user-controlled namespace storage
- support self-hosted DWN endpoint configuration
- document Enbox implementation patterns

## Phase 6: Sharing

- share one route
- export/import collection
- public read-only collections
- private shared collections
- subscription updates

## Phase 7: Productization

- onboarding polish
- pricing model
- billing
- account recovery
- security review
- landing page
- public beta

## Near-Term Technical Decisions

- Browser extension first or web app first?
- React, Svelte, or another frontend stack?
- Hosted resolver domain and route syntax?
- Local store implementation?
- Route ID format?
- Initial DWN endpoint?
- Whether to reserve `nav/` terminology or use a different command word?
- Which Enbox subscription APIs should be exercised in v0?
