# MASTER BOOTSTRAP v8 — STAGE 3
## Manifest Reconciliation & Re-Issue + Phase 3 Content Expansion Start Options

PROJECT: The World Beneath  
Authority: MASTER CONTROL v4  
SaveVersion: v9 (ACTIVE — MUST NOT CHANGE)  
Determinism: REQUIRED — REPLAY IDENTICAL  
Date: 2026-03-13

---

### HARD START

This stage may ONLY:
- compare the current `CODEBASE_MANIFEST_v12.md` (or later) against `Scripts.zip`
- identify structural drift (missing/new files, renamed files, moved files)
- re-issue an updated manifest (increment version) **if drift exists**
- rehydrate and restate the current Phase 3 authority files
- present three valid Phase 3 content-expansion start areas
- ask for approval to begin one approved start area

This stage MUST NOT:
- implement gameplay features
- alter determinism rules
- change SaveVersion
- modify C# source

---

### REQUIRED INPUT

- Latest `Scripts.zip`
- Current manifest referenced by `MASTER_LATEST_v22.md` (expected: `CODEBASE_MANIFEST_v12.md` or later)
- `PHASE_3_CONTENT_EXPANSION_START_v1.md` (or later)
- `PHASE_2_CLOSEOUT_PHASE_3_HANDOFF_v1.md` (or later)

If either Phase 3 authority file is missing → ⛔ **BLOCKED**.

---

### REQUIRED ACTIONS

1) **Diff manifest vs codebase**
   - Identify:
     - files present in code but missing from manifest
     - files listed in manifest but missing in code
     - moved / renamed paths
     - duplicated / obsolete manifest entries

2) **Confirm baseline expectations match**
   - SaveVersion: v9
   - SystemConsole baseline expected: **691 / 691 GREEN**
   - Selector + dungeon runtime + boss loop + reward claim + Craft Create + catalyst closure + alpha-prep surfaces are present and referenced in critical change zones
   - Phase 1 and 2 are structurally complete enough
   - Phase 3 content expansion is the active priority

3) **Re-issue manifest ONLY IF drift exists**
   - New version number: `CODEBASE_MANIFEST_v13.md` (or next unused)
   - Update `MASTER_LATEST` pointers accordingly in a new versioned file
   - Do not edit historical manifests; add a new version

4) **Open and restate the active Phase 3 authority**
   - Confirm the Phase 3 files are present and readable
   - Restate Phase 3 in compact form:
     - engine/foundation is structurally complete enough
     - content expansion is now the primary focus
     - narrow engine corrections remain allowed when content reveals real seams

5) **Present exactly three valid Phase 3 start areas**
   - Restate the three start options in compact form and tie each to current certified systems.

   **Phase 3 Start Area A — Content Pool Expansion**
   - expand active pet / monster / skill / modifier output pools
   - increase craftable output breadth using the current live authorities
   - deepen variety without changing the core loop doctrine

   **Phase 3 Start Area B — Dungeon Content Expansion**
   - expand biome / family / encounter variety
   - add more meaningful run-content breadth on top of the certified selector + preview + runtime loop
   - preserve current boss scheduling / reward authority

   **Phase 3 Start Area C — Progression & Economy Expansion**
   - expand exact recipe coverage and reward-to-output relationships
   - deepen progression texture across Will / materials / catalysts / craft outputs
   - preserve the current closed Tier 1 loop while adding breadth

6) **Lock the immediate next step format**
   - Ask the user to choose one of the three Phase 3 start areas
   - Require that the next implementation/audit window be framed narrowly under the chosen area
   - Do not pre-commit the user to a fixed long chain unless they explicitly want one

7) **Prepare Stage-3 output**
   - If a new manifest is issued:
     - new manifest filename
     - list of structural changes (paths only)
     - updated pointer instructions for `MASTER_LATEST_v22.md` (or later)
   - End by:
     - restating that the Phase 3 files are now part of the active master-window authority set
     - asking for approval to begin one of the three Phase 3 start areas

---

### REQUIRED OUTPUT (IN-CHAT)

- Drift summary (if any)
- If a new manifest is issued:
  - new manifest filename
  - list of changes (paths only)
  - updated pointers in `MASTER_LATEST`
- Confirmation that the Phase 3 authority files were found and re-locked into the session authority set
- Compact restatement of the three valid Phase 3 start areas
- Recommended first next track as a **choice**, not a forced sequence:
  - **A — Content Pool Expansion**
  - **B — Dungeon Content Expansion**
  - **C — Progression & Economy Expansion**
- Final explicit approval question:
  - **Approve starting Phase 3 in Area A, B, or C?**

---

### TERMINATION LINE (exact)

**MASTER BOOTSTRAP v8 — COMPLETE. AUTHORITY REHYDRATED. PHASE 3 LOCKED. AWAITING APPROVAL TO START AREA A, B, OR C.**
