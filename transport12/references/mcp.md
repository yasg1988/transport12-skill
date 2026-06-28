# MCP Integration

Use this reference when changing `transport12-mcp`.

## Boundary

- MCP clients call only the transport12 HTTP API.
- Do not reimplement direct data-source parsing in MCP.
- Do not include favorites, language selection, localized answer generation, main menus, or Telegram/VK button flows.
- Do not commit production base URLs or secrets.

## Tool Design

- Prefer small tools with explicit parameters.
- Return JSON text so AI clients can inspect full fields.
- Keep error messages diagnostic but avoid secrets and internal credentials.
- Use `get_service_status` for diagnostics instead of exposing source-provider details.

## Current Tool Categories

- Availability: `health`, `get_service_status`, `get_api_summary`.
- Stops: `search_stops`, `find_nearby_stops`, `get_stop_routes`, `get_stop_arrivals`.
- Routes: `search_routes`, `get_route`, `get_route_stops`.
- Vehicles: `get_route_vehicles`, `get_vehicle_forecast`.
- Bus station: `search_bus_station_destinations`, `get_bus_station_races`, `get_ticket_url`.
- Cross-search: `search_everything`.

## Adding Tools

1. Add the tool in `src/tools.ts`.
2. Reuse `Transport12ApiClient` from `src/api.ts`.
3. Update README tool list.
4. Add smoke coverage when the tool checks API health or core behavior.
5. Run `pnpm run build`.
