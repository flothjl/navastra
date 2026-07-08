# Enbox Reference App

Navastra is intended to be a reference app for Enbox.

The goal is not only to build a useful personal navigation tool. The goal is to
show how a consumer app can use Enbox for identity, storage, sync, and portable
application data without making users think about infrastructure.

## Why Navastra Fits Enbox

Navastra has a simple but meaningful data model:

- route records
- collection records
- local cache
- multi-device sync
- scoped sharing later

That makes it a good reference app because the product is easy to understand
while still exercising important Enbox capabilities.

## Enbox Capabilities To Demonstrate

### Typed Protocols

Navastra should define a route protocol with typed route and collection records.

This should demonstrate:

- protocol definition
- schema evolution
- encrypted record types
- queryable tags
- app-specific access rules

### Record CRUD

Every core product action should map cleanly to Enbox records:

- create route
- query routes
- update destination
- rename route
- delete route
- create collection
- add route to collection

### Session Restore

Users should be able to return to Navastra and see their namespace without
restarting identity setup.

### Local-First UX

The route cache should make resolution instant, but the cache should be derived
from Enbox records. Enbox is the source of truth; the cache is the performance
layer.

### DWN Sync

The MVP should sync route records through a development DWN endpoint. Later
versions should support self-hosted DWN endpoints.

### Subscriptions

If Enbox subscriptions are stable enough, route manager views should update when
records change. This is especially useful for multi-device and shared
collection flows.

## Reference App Constraints

- Do not build a parallel hosted data model that competes with Enbox.
- Do not require users to understand DIDs, DWNs, or protocols during onboarding.
- Do expose enough developer documentation that Enbox users can learn from the
  app.
- Do keep JSON export/import so the data shape is easy to inspect.
- Do keep a local route cache so the address-bar experience stays fast.

## Suggested First Build

1. Web app route manager.
2. Enbox connect/session restore.
3. Navastra route protocol.
4. Route CRUD backed by Enbox records.
5. IndexedDB route cache hydrated from Enbox records.
6. Browser extension that resolves from the local cache.
7. JSON export/import for debugging and portability.

## Success Criteria

Navastra succeeds as an Enbox reference app if it proves:

- Enbox can support a polished consumer workflow.
- Typed protocols make application data understandable.
- DWN-backed sync can feel normal to users.
- Ownership can be a product advantage without becoming heavy UI copy.
- Developers can copy patterns from Navastra into their own Enbox apps.
