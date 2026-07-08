# Data Model

The data model should be small, explicit, and portable.

## Route

A route maps a memorable name to a destination.

```json
{
  "id": "route_01JZ0000000000000000000000",
  "name": "budget",
  "destination": {
    "type": "url",
    "url": "https://example.com/spreadsheets/household-budget"
  },
  "title": "Household Budget",
  "description": "Main budget spreadsheet",
  "tags": ["finance", "home"],
  "collectionIds": ["collection_personal"],
  "createdAt": "2026-07-07T00:00:00.000Z",
  "updatedAt": "2026-07-07T00:00:00.000Z"
}
```

## Route Fields

- `id`: stable unique identifier
- `name`: user-facing alias
- `destination`: target action, initially URL-only
- `title`: readable display name
- `description`: optional note
- `tags`: optional labels for search and organization
- `collectionIds`: optional grouping
- `createdAt`: creation timestamp
- `updatedAt`: last update timestamp

## Name Rules

Initial route names should:

- use lowercase letters, numbers, dashes, underscores, and slashes
- be case-insensitive at resolution time
- trim leading and trailing slashes
- reject empty segments
- avoid whitespace

Examples:

```text
budget
docs/api
github/navastra
home/router
work/payroll
```

## Destination Types

V0 should only require URL destinations.

Future destination types may include:

- search templates
- local files
- app deep links
- mailto links
- command actions
- collection landing pages

## Collection

A collection groups routes for import, export, sharing, or display.

```json
{
  "id": "collection_personal",
  "name": "personal",
  "title": "Personal",
  "description": "Default personal namespace",
  "visibility": "private",
  "createdAt": "2026-07-07T00:00:00.000Z",
  "updatedAt": "2026-07-07T00:00:00.000Z"
}
```

## Usage Event

Usage should be local by default. If remote analytics are ever added, they
should be opt-in.

```json
{
  "routeId": "route_01JZ0000000000000000000000",
  "resolvedAt": "2026-07-07T00:00:00.000Z",
  "source": "extension"
}
```

## Export Format

The export format should be plain JSON:

```json
{
  "schema": "navastra.routes.v1",
  "exportedAt": "2026-07-07T00:00:00.000Z",
  "routes": [],
  "collections": []
}
```

## Sync Notes

The route schema should be storage-neutral. Hosted sync, local files, and
DWN-backed storage should all be able to read and write the same logical data.
