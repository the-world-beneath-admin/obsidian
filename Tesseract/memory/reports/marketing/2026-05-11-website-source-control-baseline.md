# Website Source-Control Baseline Report - 2026-05-11

## Task

Repair the website source-control baseline after the approved homepage deployment so future public-site changes do not depend on an uncommitted dirty working tree.

## Result

Created a local Git baseline branch for the current production-source state:

```text
Branch: codex/website-production-baseline-20260511
Commit: f510e2b
Message: chore: establish production website baseline
Repo: C:\Users\yrred\Desktop\Markeing\Websites\the-world-beneath-site
```

This branch was created from the previous local branch:

```text
codex/archaeology-release-ready-step8
```

The baseline commit preserves the production-source state that matches the deployed isolated workspace, while leaving the older archaeology branch available in Git history.

The branch was pushed to GitHub and opened as a draft PR:

```text
PR: https://github.com/dodo-arcforge-interactive/the-world-beneath-site/pull/1
State: Merged
Base: main
Head: codex/website-production-baseline-20260511
Merge commit: d39958b1e546b506e3e903fa91663ec57ae8a5a8
Merged at: 2026-05-11T21:59:31Z
```

Local `main` was fast-forwarded to the merge commit.

## Files touched

The baseline commit records the full current website source-control state:

- 704 files changed
- 57,197 insertions
- 2,265,280 deletions
- New local ignore rule: `*.log` in `.gitignore`

The large deletion count is mostly removed archaeology/map/storyline content that existed in the previous branch state but was not present in the production-source candidate used for deployment.

## Checks run

- Confirmed the dirty source folder and isolated deployment workspace were byte-for-byte identical when excluding `.git`, `.wrangler`, and `.log` files before the `.gitignore` housekeeping edit.
- After the baseline commit, the only intentional deploy-irrelevant difference from the isolated workspace is the new `.gitignore` `*.log` rule.
- Confirmed Git branch is clean after the commit.
- Confirmed approved hero line exists in committed `index.html`.
- Ran `npx wrangler deploy --dry-run` from the committed source branch before and after pushing the branch.
- Dry-run result:

```text
Total Upload: 180.63 KiB / gzip: 34.23 KiB
```

- Rechecked the live site at `https://the-world-beneath.com/` and confirmed the deployed homepage copy is still present.
- Confirmed GitHub draft PR #1 is open with head `codex/website-production-baseline-20260511` and base `main`.
- User confirmed the website wiki additions should remain in the baseline.
- Marked PR #1 ready and merged it into `main`.
- Fast-forwarded local `main` to `origin/main`.
- Ran `npx wrangler deploy --dry-run` from local `main`; result remained `180.63 KiB / gzip: 34.23 KiB`.

## Risks

- PR #1 has been merged into `main`; future website work should start from updated `main`.
- The commit is intentionally large because it captures the true current source state, not a small copy-only patch.
- The remote `origin/main` may still represent an older website state and should not be treated as production baseline without review.
- Future deploys should use this baseline branch or a reviewed successor branch, not the old dirty working-tree state.
- User confirmed the archaeology, archaeology story, Bob Forge, and archaeology map deletions are acceptable and should not be restored.
- The remaining merge question is wiki scope: the PR adds website wiki-related files but does not delete wiki files.

## Memory-worthy notes

### Decision - 2026-05-11

The local website production baseline is now represented by branch `codex/website-production-baseline-20260511` at commit `f510e2b`.

### Warning - 2026-05-11

Do not deploy from `origin/main` or the older archaeology branch without confirming they contain the current live-site structure and homepage copy.

### Decision - 2026-05-11

The production baseline branch was pushed and opened as a draft PR for review: `https://github.com/dodo-arcforge-interactive/the-world-beneath-site/pull/1`.

### Decision - 2026-05-11

The user approved the removal of old archaeology, archaeology story, Bob Forge, and archaeology map material. Do not restore that old material as part of the baseline review.

### Decision - 2026-05-11

The user approved keeping the website wiki additions in the production baseline.

### Decision - 2026-05-11

Draft PR #1 was merged into `main`; merge commit `d39958b1e546b506e3e903fa91663ec57ae8a5a8` is now the remote and local website baseline.

## Follow-up recommendations

1. Use updated `main` as the starting point for the next website or SEO deployment.
2. Create a focused branch for the next site/SEO change.
3. Run dry-run and route checks before any future public deploy.
4. Consider adding a lightweight deployment checklist script later so future copy-only deploys can verify allowed changed files automatically.
