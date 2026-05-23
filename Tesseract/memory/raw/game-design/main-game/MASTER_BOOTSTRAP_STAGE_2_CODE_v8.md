# MASTER BOOTSTRAP v8 — STAGE 2
## Codebase Rehydration — Read Only (Phase 3 Content Expansion Start)

PROJECT: The World Beneath  
Authority: MASTER CONTROL v4  
SaveVersion: v9 (ACTIVE — MUST NOT CHANGE)  
Determinism: REQUIRED — REPLAY IDENTICAL  
Date: 2026-03-13

---

### HARD START

No implementation.  
No C# output.  
Read-only verification only.

If `Scripts.zip` missing → ⛔ **BLOCKED**.

---

### REQUIRED INPUT

Upload `Scripts.zip` (latest compiling version) AND confirm:

- Compilation baseline is GREEN in Unity
- Unity Console is CLEAR
- SystemConsole baseline is GREEN (record exact count)
- SaveVersion remains v9 unchanged
- No `*.ApplyV2.cs` partial files exist

---

### REQUIRED ACTIONS (READ-ONLY)

1) **Verify current runtime foundations exist**
   - dungeon selector / staged tuple surfaces
   - dungeon preview / matrix projection surfaces
   - dungeon runtime loop surfaces
   - boss scheduling / boss reward surfaces
   - loot runtime / claim / inventory surfaces
   - Craft Create authority surfaces
   - Apply / selection / inventory surfaces

2) **Verify current progression loop surfaces exist**
   - Will / material / catalyst reward flow
   - craft execution path
   - crafted output routing into inventory
   - catalyst-driven pet-card resolution through active Tier 1 pools
   - starter-party support surfaces for repeatable testing

3) **Verify current content-expansion-relevant surfaces exist**
   - pet-card/support registries
   - mirrored monster/content registries
   - family / biome / affinity support registries
   - recipe discovery / fallback / catalyst pool surfaces
   - reward-family / catalyst-family mapping surfaces
   - UI builders most likely to be touched during Phase 3 content work

4) **Verify SystemConsole coverage includes the post-alpha-prep baseline**
   - selector certification tests
   - dungeon runtime loop tests
   - boss loop / boss loot tests
   - Craft Create authority tests
   - catalyst closure tests
   - alpha readiness cleanup tests
   - current baseline expected: **691 / 691 GREEN**

5) **Identify codebase drift vs current manifest**
   - files present in code but missing from manifest
   - files listed in manifest but absent in code
   - moved / renamed paths
   - Phase-3-relevant surfaces that the manifest must mention

---

### REQUIRED OUTPUT (IN-CHAT)

Produce a short **Codebase Rehydration Report** containing:
- confirmed presence of the key selector + dungeon + boss + loot + craft + apply files (actual paths)
- confirmed presence of current content-expansion-relevant registries / authorities
- SystemConsole baseline observed (exact count)
- any drift vs current manifest (report only; no edits)

---

### TERMINATION LINE (exact)

**MASTER BOOTSTRAP v8 — STAGE 2 COMPLETE. READY FOR STAGE 3 (MANIFEST RECONCILIATION + PHASE 3 START OPTIONS).**
