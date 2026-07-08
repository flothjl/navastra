# Roadmap

## Phase 0: Documentation And Decisions

- define product brief
- define MVP scope
- define route schema
- decide first address-bar workflow
- choose first client stack
- choose sync strategy for prototype

## Phase 1: Local Prototype

- web app route manager
- local route store
- create, edit, delete, search routes
- JSON import/export
- hosted-style resolver route in development
- manual testing with seed routes

## Phase 2: Browser Extension

- extension keyword support
- local cache
- redirect flow
- not-found page
- route creation shortcut from current tab
- background sync from web app storage

## Phase 3: Import And Portability

- browser bookmark import
- import review screen
- route name suggestions
- Markdown export
- route schema versioning
- backup and restore

## Phase 4: Sync

- sync adapter interface
- hosted sync prototype
- conflict handling rules
- local cache invalidation
- multi-device smoke testing

## Phase 5: Ownership Layer

- evaluate DWN-backed storage
- evaluate Enbox integration
- define identity and authorization model
- support user-controlled namespace storage
- document migration path from hosted sync to user-controlled sync

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
- Initial sync provider?
- Whether to reserve `nav/` terminology or use a different command word?
