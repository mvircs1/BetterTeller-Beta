# BetterTeller

Storyteller AI mod for RimWorld.

## Setup
- Copy `Directory.Build.props.template` to `Directory.Build.props` and edit it.
  - `RimWorldDir` should point to the RimWorld game folder.
  - `HarmonyDir` should point to the Harmony mod `Assemblies` folder.
- Ensure the Harmony mod is present at the configured location.
  - `Directory.Build.props` is local-only and should not be committed.

## Build
```powershell
.\build\scripts\build.ps1
```

Build output: `mod/Assemblies/BetterTeller.dll`.

## How BetterTeller decides
The AI uses a two-layer director plus learning and safety rails:
1) Feature extraction: reads colony state (wealth, threats, crisis flags).
2) Outcomes update: settles rewards from recent incidents (short + medium windows).
3) Macro mode: scores modes (Pressure/Relief/Quest/Variety/Chaos) and applies semi-Markov
   constraints (min/max duration + allowed transitions). Bandit bias is applied when learning is on.
4) Candidate pool: pulls incidents by preferred tags for the chosen mode.
5) Hard constraints (masking): blocks incidents by cooldowns, recovery lock, budget, crisis, etc.
6) Micro scoring: multi-criteria scoring (mode fit, pacing, fairness, novelty, soft constraints).
7) Top-K selection: keeps the top N incidents and samples by weight to avoid long-tail picks.
8) Execution: tries top-N with retries, applies threat point scaling, and logs failures.
9) Fallback: attempts safe categories if execution fails; otherwise returns no event.

Debug tools:
- Enable debug to see the in-game overlay (mode, budgets, top candidates, block reasons).
- Use "Dump telemetry" to log or export CSV/JSON files for analysis.

## Install (dev)
- Copy `mod/` into your RimWorld `Mods/BetterTeller` folder, or create a symlink.
- Enable the mod and select the BetterTeller storyteller in-game.

## Install (release)
- Package the mod:
```powershell
.\build\scripts\package.ps1 -Version 0.1.0
```
- The zip will be placed in `build/artifacts`.
  - Do not ship `.git/` or `src/**/obj/` in releases.
  - Use `-Release` to also copy the zip into `Release/`.

## Run
- Enable the mod and select the BetterTeller storyteller in-game.
