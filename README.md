Tactical 5v5 FPS — Roles + Impact Scoring (Godot 4)

CS-style gunplay with a round-based bomb/defuse objective.
Designed for low-elo clarity and high-elo depth using clear squad roles and an impact-based scoring system that rewards what actually swung the round (opening/trades/plant/utility), not raw K/D.

Roles: Entry · Medic · Utility Specialist (bomb) · Sniper
Engine: Godot 4.x (GDScript) · License: MIT

✨ Core Ideas

Gunplay first, no “superpowers” — roles provide subtle passives and responsibilities.

Impact scoring — a single enabling entry + plant → win should outscore a baity 4k on a lost round.

Low-elo guidance — roles + UI teach good habits (flashes for entry, plant under cover, revives that matter).

📦 What’s in this repo (MVP scope)

Godot 4 project with first-person movement & sprint/FOV.

Spec-driven design so AI coding agents (Codex) can build features consistently:

/specs/role_defs.csv — passive perks & loadout hints

/specs/impact_weights.yaml — weights/multipliers/caps/windows

/specs/events_schema.json — canonical telemetry events

/specs/gameplay_tags.txt — tag constants shared across systems

Stubs for:

addons/telemetry/EventBus.gd — centralized game event bus

addons/impact_scoring/ImpactScoring.gd — computes Impact from events

scenes/ui/Scoreboard.tscn — Impact-first scoreboard (to be implemented)

See the Roadmap for the vertical slice plan.

🧰 Requirements

Godot 4.2+ (Mono not required)

A GPU that runs Godot 4 (Vulkan)

(Optional) Git installed if you’re cloning

🚀 Quick Start

Clone or download this repository.

Open Godot 4, choose Import, and select the project folder.

Press Play ▶ to run the current scene (or set Main scene as default).

Controls (default):

WASD — Move

Space — Jump

Shift — Sprint

Esc — Toggle mouse capture

(Weapon/role/ui bindings will appear as they land in later milestones)

🗂️ Project Structure
/game (project root)
  /addons
    /roles/                # Role manager & passives (Entry/Medic/Utility/Sniper)
    /telemetry/            # EventBus (signals), JSON dev logger
    /impact_scoring/       # Impact scoring engine (weights → score)
  /scenes
    /levels/               # Greybox maps
      /annot/              # Area3D markers (Choke, Site A/B, Lanes)
    /ui/                   # Scoreboard, round recap chips
  /scripts
    /gameplay/             # Health, Teams, RoundManager, Bomb/Defuse
    /weapons/              # Weapon base + Rifle/SMG/Sniper
    /utility/              # Flash/Smoke/Molly
/specs/                    # Data-first design (CSV/YAML/JSON/tags)
/docs/                     # Design notes, contribution guide, Codex tasks

🧪 Impact Scoring (high level)

Events → (weights × multipliers) → Impact (per-round & per-match)

Key weights (tunable in /specs/impact_weights.yaml):

Opening kill at choke/site (boosted for Entry)

Trades within 3s

Man-advantage flips

Plant/defuse (bonus if under fire, plus plant → round win)

Utility assists (flash → kill ≤4s), smoke cover time, molly delays

Exit/eco frags are hard down-weighted/capped

Acceptance test:

Entry gets 1 opening at choke → plant within 12s → round win must outscore 4 exit frags in a lost round.

🧑‍⚕️ Roles (v0 passives)

Entry: +movement/sprint handling, quicker weapon ready, quieter steps. Job: take space and open sites.

Medic: limited revives + slow heals over time; XP only if revived/healed teammate survives or contributes.

Utility Specialist (bomb): auto-carries bomb, +1 nade slot, discounted nades, faster plant/defuse.

Sniper: faster scope-ready, steadier hold; Job: picks & overwatch.

All weapons/utilities remain universal; roles nudge behavior via passives and scoring.

🧭 Roadmap (vertical slice)

M1 – Core Shooter: weapons (hitscan), health/damage, death/downed
M2 – Bomb/Defuse Mode: Teams, Sites A/B, RoundManager
M3 – Level Annotations: Area3D volumes for Zone.Choke, Zone.Site, lanes
M4 – Roles Framework: RoleManager + passives; Specialist auto-bomb
M5 – Utilities: Flash (LOS & blind window), Smoke (execute window), Molly (deny/delay)
M6 – Telemetry EventBus: emit Kill/Trade/Plant/Defuse/Utility/ZoneCross with context
M7 – Impact Scoring: apply weights/multipliers/caps; CSV dump tooling
M8 – Scoreboard UI: Impact big; K/D small; role breakdown; round recap chips
M9 – Simple Bots: generate events to tune weights
M10 – Tuning Harness: console cmds reload_impact_weights, dump_impact_csv

🤖 Using an AI coding agent (Codex)

This repo is structured for agent workflows.

Open the tasks in /docs/CODEX_TASK.md (create if missing) and the issues named:

M1: Core Shooter – Weapons & Health, … through M10 (see Roadmap).

Ask the agent to:

Work the milestones in order.

Keep new code in the specified folders.

Wire all gameplay events through EventBus.gd.

Make Impact pass the acceptance test above.

You review PRs using the checklist below.

PR Checklist

 No Godot warnings/errors on run.

 Roles feel subtle (no hero abilities).

 Telemetry events include context (pre/post-plant, trade ≤3s, execute window).

 One enabling entry → plant → win out-scores bait 4k on loss.

 Scoreboard highlights non-frag roles when they swing rounds.

🧪 Handy test scenes (ask for these in PRs)

Entry Test: Flash → entry kill at choke → plant ≤12s → round win

Bait Test: 4 late kills after save call → round loss

Medic Test: Revive → revived survives ≥10s or gets a kill

Specialist Test: Smoke covers plant lane; plant under fire; plant leads to win

Sniper Test: Opening pick on execute lane stalls rotate ≥7s

🐛 Troubleshooting

Mouse not captured? Press Esc to toggle capture.

Low FPS in editor? Disable MSAA in Project Settings while developing.

No events in log? Ensure EventBus is autoloaded and listeners are connected.

🤝 Contributing

Fork → feature branch → PR.

Keep functions small; add docstrings; prefer data in /specs/ where possible.

Include a short demo clip or GIF for UI/gameplay changes when you can.

📜 License

MIT — do whatever, just keep the copyright notice.

🙏 Acknowledgements

Built on a Godot 4 FPS starter template (MIT) and extended for role-based, impact-scored tactical play.

Thanks to the open-source Godot community for tools, examples, and docs.

Questions or ideas? Open an issue with the tag design or question.
