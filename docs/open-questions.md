# Open Questions

## Naming

- Is Navastra the long-term product name or only a working name?
- Should the command syntax use `nav`, `go`, `n`, or another keyword?
- Should route names be called routes, glyphs, marks, aliases, or links?

## Product

- Is the first customer a power user, developer, or non-technical consumer?
- Is the first wedge individual productivity or small-group sharing?
- Should bookmark import be in the first release?
- Should the product include public pages for shared collections?
- Should usage history be local-only by default?

## Technical

- What is the first browser target?
- Can the extension own the Enbox session directly, or should the web app own
  session lifecycle and publish a cache to extension storage?
- Which DWN endpoint should be used for development?
- How should route names be indexed for fast lookup while keeping route data
  encrypted?
- Should route cache hydration use query-on-load, subscriptions, or both?

## Identity And Ownership

- What does account recovery look like if routes belong to the user?
- How much identity detail should be visible in the UI?
- How are shared collections authorized and revoked?
- How should self-hosted DWN endpoints be configured in the UI?

## Business

- Is this a paid consumer utility, a prosumer tool, or a hosted service around
  open-source clients?
- What feature justifies payment?
- Should teams be supported later, or avoided to stay consumer-focused?
- What is the simplest pricing model?

## Risks

- Browser address-bar behavior may limit the ideal syntax.
- Users may not want another extension.
- Bookmark import may create noise instead of clarity.
- Enbox API changes may affect the reference app while the platform is still in
  research preview.
- DWN sync complexity may slow down the first address-bar validation loop.
- Naming may need formal clearance before public launch.
