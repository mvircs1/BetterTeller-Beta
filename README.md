# BetterTeller

BetterTeller is a custom storyteller AI for RimWorld that selects and schedules incidents
using a director-style pipeline with macro/micro scoring, hard safety rules, and learning.
AI roles: Brain = Contextual Bandit (Thompson Sampling), Director = Belief State + Homeostatic Pacing + Action Masking, Executor = Hierarchical Utility AI (Macro/Micro) + Top-K selection.

## Install (RimWorld)
1) Copy the `mod` folder to `RimWorld/Mods/BetterTeller`.
2) Make sure the final structure looks like:
```
RimWorld/Mods/BetterTeller
  About/
  Assemblies/
  Defs/
  Languages/
  Patches/
```
3) Launch RimWorld and enable the mod in the Mods menu.
4) Start or load a game and select the BetterTeller storyteller.
