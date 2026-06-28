# API Contracts

Use this reference when changing transport12 API behavior or MCP tools that consume it.

## Dates

- Bus station race dates use `dd.mm.yyyy`.
- API clients must not guess a date when the user explicitly gives one.
- If no date is supplied for bus station races, the main API may use its default date behavior.

## Coordinates

- `lat` and `lng` are decimal numbers.
- Nearby stop lookup uses `GET /api/v1/stops/near?lat=...&lng=...`.

## Stops

Stop records usually contain:

- `id`
- `name`
- `description`
- `lat`
- `lng`
- `direction`

Stop arrival records from `/api/v1/stops/:stationId/forecast` are treated as factual arrival data in user interfaces.

## Routes

Normalized route records usually contain:

- `id`
- `label`
- `kind`
- `number`
- `shortName`
- `fromStation`
- `toStation`

Route kind is a normalized transport category. Do not expose source-provider enum names in companion clients.

## Vehicles

Vehicle records may contain device identifiers, route identifiers, coordinates, speed, direction, and update time.

Use `deviceCode` from `/api/v1/vehicles` with `/api/v1/vehicles/:deviceCode/forecast`.

## Bus Station Races

Race records usually contain:

- `raceId`
- `routeName`
- `departureTime`
- `arrivalTime`
- `departurePoint`
- `arrivalPoint`
- `freeSeats`
- `totalSeats`
- `priceRub`
- `buyUrl`
- `scheduleUrl`

Use `buyUrl` first when present. Fall back to `scheduleUrl` for a compact route page link.

## Bus Station Calendar

Calendar records are aggregated by transport12 from race lookups.

Calendar requests support:

- `destinationId`
- `from` in `dd.mm.yyyy`
- `to` in `dd.mm.yyyy`
- `days` when `to` is omitted

The date range is capped to the source-supported future window. Calendar day records contain:

- `date`
- `hasRaces`
- `raceCount`
- `firstDepartureTime`
- `minPriceRub`
- `freeSeats`
- `totalSeats`
- `scheduleUrl`
