---
name: floor-plan-to-3d
description: Floor plan to 3D with VEDUTUM. Use when someone wants to turn an architectural floor plan (PDF, JPG, PNG) into a measured 3D model, needs rooms and areas from a plan, wants a house furnished, a roof, facade or solar layout set, or a share link for a client — with the VEDUTUM MCP server (tools vedutum_*).
---

# Floor plan to 3D with VEDUTUM

VEDUTUM reads architectural floor plans into a measured model (walls, openings, rooms in metres) and builds the 3D model from it. The MCP server `vedutum` (https://www.vedutum.com/mcp) has public tools and tools on the person's own VEDUTUM account. The first account tool asks for sign-in: run `/mcp`, choose `vedutum`, sign in with the VEDUTUM account (or open one — 30 days free) and allow the connection.

## The usual path

1. **Find or create the project.** `vedutum_list_projects` (ids, plan state, points left). For a new one `vedutum_create_project` with title, optional client and site address.
2. **Get the plan in.** The plan must be one storey per sheet.
   - A file that is online: `vedutum_read_floor_plan` with `project_id`, a direct https `file_url` (not a preview page) and `storey` (0 ground floor, 1 first floor, -1 basement). Costs 1 point per storey — say so before calling it.
   - A file on the person's computer: Claude Code cannot upload it to the server. Give them the upload link from `vedutum_get_project` (`uploadUrl`); the reading then runs in the app.
   - Unsure whether the file works: `vedutum_check_floor_plan` (file type, size, scan or CAD, scale) — public, free.
3. **Wait for the reading** (one to three minutes), then `vedutum_get_project`: plan status, storeys, rooms with approximate areas, outline area per storey and in total. If a reading failed, the error says why (wrong page, no scale, too large); fix the file and read again.
4. **Shape the model** (each change can be taken back one step with `vedutum_undo_last_change`):
   - `vedutum_furnish_rooms` — all rooms, one storey, or one room by name; `mode: "replace"` to furnish anew.
   - `vedutum_set_design` — roof (`flat`, `gable`, `shed`), facade, frames, style, storeys, storey height, north angle.
   - `vedutum_add_solar` — PV or solar thermal on the roof faces not facing north; reports modules and kWp (rated power, not yield).
   - `vedutum_set_site_address` — sun position plus neighbouring buildings and terrain from OpenStreetMap.
5. **Share** with `vedutum_share_link`: the client sees model and pictures, comments and approves without an account.

## Good to know

- Images and videos are made in the VEDUTUM app, never through these tools; link the person to the project URL the tools return.
- Areas from `vedutum_get_project` are estimates from the drawing (room rectangles, outline), not a certified living-area calculation — say so when you quote them.
- When points or the free month have run out, the tool answers with the reason and the link to the plans page; pass that on, do not retry.
- Public tools without an account: `vedutum_estimate_points`, `vedutum_sun_and_shadow`, `vedutum_print_resolution`, `vedutum_search_knowledge`, `vedutum_example_project`, `vedutum_get_started`, and `vedutum_view_model` (example house in 3D; in hosts with MCP Apps it renders inline).
- Answer in the person's language; the tools take `language: "de"` or `"en"`.
