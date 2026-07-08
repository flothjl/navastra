# Roadmap

## Phase 0: Documentation And Decisions

- define product brief
- define MVP scope
- define route schema
- lock extension-first omnibox workflow
- choose first client stack
- define Enbox route protocol
- choose development DWN endpoint
- document concrete Enbox package/API choices

## Phase 1: Extension MVP

- browser extension scaffold
- omnibox keyword support
- exact-match redirect flow
- not-found and suggestions flow
- compact resolver cache
- web app route manager opened from the extension
- Enbox connect/session restore
- Enbox-backed route store
- create, edit, delete, search routes through Enbox records
- resolver cache hydrated from Enbox records
- JSON import/export
- manual testing with seed routes

## Phase 2: Import And Cache Polish

- route creation shortcut from current tab
- cache hydration from Enbox records
- browser bookmark import
- import review screen
- route name suggestions
- Markdown export
- route schema versioning
- backup and restore

## Phase 3: Enbox Sync

- development DWN sync
- conflict handling rules
- local cache invalidation
- multi-device smoke testing
- subscription-driven route manager updates

## Phase 4: Hosted Resolver And Sharing

- hosted resolver fallback
- share one route
- export/import collection
- public read-only collections
- private shared collections
- subscription updates

## Phase 5: Ownership Layer Polish

- define identity and authorization model
- support user-controlled namespace storage
- support self-hosted DWN endpoint configuration
- document Enbox implementation patterns

## Phase 6: Productization

- onboarding polish
- pricing model
- billing
- account recovery
- security review
- landing page
- public beta

## Near-Term Technical Decisions

- React, Svelte, or another frontend stack?
- Hosted resolver domain and route syntax?
- Local store implementation?
- Route ID format?
- Initial DWN endpoint?
- Whether to use `nav` as the omnibox keyword or pick a shorter command word?
- Which Enbox subscription APIs should be exercised in v0?
