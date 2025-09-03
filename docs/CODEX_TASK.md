# Project: Tactical 5v5 FPS (Godot 4) with Squad Roles + Impact Scoring

## Vision
CS-style gunplay and bomb/defuse objective. Four squad roles:
- Entry (movement/space taking)
- Medic (heals/revives)
- Utility Specialist (bomb carrier + utility economy; faster plant/defuse)
- Sniper (overwatch; faster scope-ready)

Scoring rewards *round-swinging* actions (opening & trades, space taken, plant/defuse, utility-enabled kills), not raw K/D.

## Ground Rules
- Engine: **Godot 4.x** (GDScript).
- License: **MIT**. Keep code clean; no external code unless MIT-compatible.
- Scope: **Local play first** (singleplayer + splitscreen acceptable), optional local multiplayer later.
- Keep everything deterministic & server-authoritative ready (even if singleplayer now).

## Deliverables (order matters)
1) **Core shooter**: weapons, health/damage, basic TTK.
2) **Bomb/defuse mode**: teams, sites (A/B), round loop.
3) **Roles**: passive perks per role; simple role picker.
4) **Utilities**: flash/smoke/molly with minimal but correct logic.
5) **Telemetry & Impact scoring**: event bus + weighted scoring from `/specs/impact_weights.yaml`.
6) **Scoreboard UI**: “Impact” big; K/D small; per-role breakdown; round recap chips.
7) **Bots (basic)**: generate events for tuning.

## Definitions & Specs
Use the data files in `/specs/` (committed in this repo):
- `role_defs.csv` – role passives & loadout hints.
- `impact_weights.yaml` – weights, multipliers, caps, windows.
- `events_schema.json` – canonical telemetry event format.
- `gameplay_tags.txt` – tag constants used across systems.

## Acceptance Criteria (global)
- A single enabling Entry kill → site plant → round win **out-scores** a 4x exit-frag round loss.
- Utility-enabled kills grant **assist XP to Utility Specialist**, not to killer.
- Exit/garbage-time frags and eco-farms are **hard down-weighted**.

## Conventions
- New code in:
  - `addons/roles/`, `addons/telemetry/`, `addons/impact_scoring/`
  - `scripts/gameplay/`, `scripts/weapons/`, `scripts/utility/`
  - `scenes/ui/`, `scenes/levels/annot/`
- Emit telemetry via a single `EventBus` (signals) matching `events_schema.json`.
- Keep functions small; add docstrings; expose key constants at top.

## What not to build yet
- Matchmaking/MMR, inventory/skins, marketplace, networking beyond local.
