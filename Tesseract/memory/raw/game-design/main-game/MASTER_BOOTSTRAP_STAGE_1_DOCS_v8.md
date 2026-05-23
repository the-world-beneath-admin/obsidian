# MASTER BOOTSTRAP v8 — STAGE 1
## Docs Rehydration — Authority Baseline (Phase 3 Content Expansion Start)

PROJECT: The World Beneath  
Authority: MASTER CONTROL v4  
SaveVersion: v9 (ACTIVE — MUST NOT CHANGE)  
Determinism: REQUIRED — REPLAY IDENTICAL  
Date: 2026-03-13

---

### HARD START — STRICT VALIDATION

You are in a NEW MASTER window. Treat all state as unknown.

You may NOT:
- implement features
- output C# code
- modify gameplay logic
- change SaveVersion

If any required input is missing → ⛔ **BLOCKED**.

---

### REQUIRED INPUTS (DOCS)

Upload the latest **docs bundle** (the authoritative `.md.zip`) containing at minimum:

- `MASTER_LATEST_v22.md` (or later)
- `MASTER_DECISION_LOCKS_v12.md` (or later)
- `MASTER_STATE_v21.md` (or later)
- `MASTER_WINDOW_HANDOFF_v4.md` (or later)
- `CODEBASE_MANIFEST_v12.md` (or later)
- `PHASE_3_CONTENT_EXPANSION_START_v1.md` (or later)
- `PHASE_2_CLOSEOUT_PHASE_3_HANDOFF_v1.md` (or later)

Also upload the latest `Scripts.zip` ONLY IF the user intends Stage 2.

---

### REQUIRED ACTIONS (READ-ONLY)

1) **Locate the current authority pointers**
   - Open `MASTER_LATEST_v22.md` (or later) and identify:
     - current Decision Locks file
     - current Master State file
     - current Master Window Handoff file
     - current Codebase Manifest file
     - current Phase 3 start / handoff files

2) **Confirm certified pillars are present or identify doc drift**
   - selector stack certified
   - dungeon preview certified
   - dungeon runtime loop certified
   - boss scheduling certified
   - boss reward / catalyst loop repaired
   - reward claim / inventory delivery certified
   - Craft Create authority surface repaired
   - Tier 1 catalyst closure repaired
   - Tier 1 crafting closure statically certified
   - alpha-facing readiness cleanup completed
   - Phase 1 and Phase 2 marked structurally complete enough for Phase 3 content expansion

3) **Extract locked invariants (must be repeated verbatim in the new window)**
   - SaveVersion: v9 unchanged
   - Determinism: replay identical
   - UI is non-authoritative; snapshot layer is projection-only
   - No `*.ApplyV2.cs` partial files permitted
   - Skill doctrine:
     - `Skill = StateA + StateB + TargetRule + CastTime + Cooldown`
   - Modifier doctrine:
     - single-effect only
     - flat before percent
     - same-id multi-slot stacking legal
   - Pet doctrine:
     - active Tier 1 pet-card pool is authoritative
     - legacy dead-branch Warden/Hunter catalyst outputs removed from live crafting
   - Boss doctrine:
     - boss scheduling is segment-aware and authoritative
     - Boss ON => final wave of that run segment is boss
     - Boss OFF => no boss in that segment
   - Crafting doctrine:
     - Craft Create is authoritative
     - Will is the crafting currency
     - Tier 1 catalyst-only recipes must not dead-end
   - Phase doctrine:
     - Phase 1 and 2 are structurally complete enough
     - Phase 3 content expansion is now the primary focus
     - narrow engine corrections remain allowed when content reveals real seams

4) **Record the certified SystemConsole baseline expectation**
   - Current operator-certified baseline: **691 / 691 GREEN**
   - Treat this as session authority if explicitly provided by the user.

5) **Identify documentation drift**
   - Report any older master files that still reflect earlier baselines or pre-Phase-3 sequencing.
   - Report drift only. Do not fix in Stage 1.

---

### REQUIRED OUTPUT (IN-CHAT)

Produce a short **Docs Rehydration Report** containing:
- authority pointers found (filenames)
- certified baseline (SystemConsole count, SaveVersion)
- locked doctrines summarized as bullet points
- whether the Phase 3 start / handoff files are present
- any documentation drift found (report only)

---

### TERMINATION LINE (exact)

**MASTER BOOTSTRAP v8 — STAGE 1 COMPLETE. READY FOR STAGE 2 (CODEBASE READ-ONLY).**
