# transport12 API Notes

Companion projects should call the transport12 HTTP API and should not reimplement direct source-provider access.

## Response Handling

- Treat `2xx` responses as transport success.
- Treat non-`2xx` responses as tool/client errors and include the status code in diagnostics.
- Preserve JSON responses when returning data to AI clients.
- Keep user-facing summaries short; raw JSON can be useful for debugging tools.

## Stops

- `GET /api/v1/stops/search?q=QUERY` returns matching stops.
- `GET /api/v1/stops/near?lat=LAT&lng=LNG` returns nearest stops.
- `GET /api/v1/stops/:stationId/routes` returns routes serving a stop.
- `GET /api/v1/stops/:stationId/forecast` returns arrival data currently treated in UI as factual arrival.

## Routes And Vehicles

- `GET /api/v1/routes` returns normalized routes.
- `GET /api/v1/routes?kind=city-bus` filters by normalized route kind.
- `GET /api/v1/routes/:routeId/stops` returns route directions and stops.
- `GET /api/v1/vehicles?routeId=ID` returns online vehicles for a route.
- `GET /api/v1/vehicles/:deviceCode/forecast` returns upcoming stops for a vehicle.

## Bus Station

- `GET /api/v1/bus-station/destinations/search?q=QUERY` finds destination options.
- `GET /api/v1/bus-station/races?destinationId=ID&date=dd.mm.yyyy` returns trips for the selected date.
- `GET /api/v1/bus-station/calendar?destinationId=ID&from=dd.mm.yyyy&days=31` returns race availability by date.
- Ticket purchase links, when present, should be shown as buttons or compact links.
