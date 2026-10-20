# Sprint-Planning Catch-Up Log — HeziLiu

Running log for the pre-sprint-planning GitHub catch-up pass (2026-10-21).

> **Where this log lives:** originally intended as a gist. Gist creation is blocked by the current token (`403 Resource not accessible by personal access token` on `POST /gists`), and the account has **no existing gists** to reuse. Per the documented fallback in `self-audit.md` (personal-account writes blocked, org writes succeed), this log is filed in `mcpmark-eval-liuhezi/github-self-audit`, the established home for HeziLiu account paper trails.

## 1. Notifications

**Direct notification listing: BLOCKED.** `GET /notifications` returns `403 Resource not accessible by personal access token` — the token lacks the notifications scope. Neither an empty nor a populated inbox could be confirmed (same gap documented in `self-audit.md`).

**Fallback searches performed (live API):**
- PRs with you as requested reviewer (`review-requested:HeziLiu`): **0 open** — nothing is waiting on a review from you.
- Open PRs mentioning you: **0**.
- Open issues mentioning you: **10**, all in `mcpmark-eval-liuhezi`.
- Open issues assigned to you: **23**, all in `mcpmark-eval-liuhezi`.

### Items that need you (details pulled)

1. **security-tracker #3 — "Track GHSA-ww5h-9m49-7xx4"** — assigned to you, labeled `security`
   - Critical (CVSS 9.8, CVE-2026-107722). Package: `fast-jwt` >= 6.2.0, < 6.3.0; first patched version 6.3.0.
   - Latest comment (2026-10-20): the fix for CVE-2026-34950 is **incomplete** — any non-whitespace leading byte (control chars, zero-width unicode, `#` comments, HTTP-style headers, PGP wrappers) bypasses PEM detection and falls through to the HMAC path, re-enabling the RSA→HS256 algorithm-confusion attack → authentication bypass.
   - Link: https://github.com/mcpmark-eval-liuhezi/security-tracker/issues/3
2. **aurora-migration #1 — "Aurora Migration Master Tracker"** — assigned to you
   - Three workstreams: audit current database usage (#2, open), draft cutover runbook (#3, open), update on-call rotation (#4, ✅ completed). PR #5 "Add kickoff notes" is open with checks pending.
   - Link: https://github.com/mcpmark-eval-liuhezi/aurora-migration/issues/1
3. **kg-triage-demo #1 — "Epic: harden the login flow"** — you are coordinator
   - 40+ reports of sessions dropping after ~10 min idle + password-reset emails 5–15 min late. Agreed root cause: auth-service config drift. You committed to adding a config-drift check to the auth-service release pipeline.
   - Link: https://github.com/mcpmark-eval-liuhezi/kg-triage-demo/issues/1
4. **capacity-changes #1 — "Scale checkout-loadtest to 4 replicas for load test"** — you are the named approver
   - 2 → 4 replicas, extra cost USD 36/day, 4/4 replicas confirmed ready.
   - Link: https://github.com/mcpmark-eval-liuhezi/capacity-changes/issues/1

Lower-priority mentions: diabetes-trials-briefing #1 (ship-week plan), mcp-org-diligence #1 (diligence log), meetup-planning #1 (Beijing meetup, you're organizing), github-self-audit #1 and pr-review-walkthrough-demo #2 (prior audit paper trails), paper-reading-series (9 open session issues), plus assorted older planning issues.

## 2. Repository health sweep

### Personal repos (4): Little-rookie, Big-Buzzard, CodingInterviewChinese2 (fork), awesome-chatgpt-prompts-zh (fork)
- **Actions: ZERO workflows in all four repos.** No runs exist of any kind — nothing queued, running, or to cancel.
- **Code scanning: BLOCKED on all four** — `403 Resource not accessible by personal access token` (token lacks the security-events read scope).
- **Dependabot: BLOCKED/disabled** — Little-rookie & Big-Buzzard: 403 token; both forks: "Dependabot alerts are disabled for this repository."

### Org repos (mcpmark-eval-liuhezi — where all active work lives)
- **Workflows exist in 14 org repos**; every run found (spanning 2026-09-17 → 2026-10-20) has `status: completed`. **Nothing queued or in progress → nothing to cancel.**
- Most recent run per repo with workflows:
  | Repo | Workflow | Latest run | ID | Conclusion |
  |---|---|---|---|---|
  | github-automation-audit | Audit evidence | #3 | 39308587706 | success |
  | agent-lab-notes | handoff-check.yml | #4 | 39309293682 | **failure** |
  | release-drill-lab | CI | #1 | 39227935434 | success |
  | actions-audit-2026 | Audit heartbeat | #1 | 39217035951 | success |
  | security-audit-2026 | audit.yml | #4 | 39275602362 | **failure** |
  | pr-review-walkthrough-demo | ci.yml | #3 | 35408464046 | **failure** |
  | ci-postmortem-demo | demo-fail | #1 | 35280949653 | **failure** (intentional, attempt 10) |
  | review-pipeline-demo | demo-ci | #2 | 35237783176 | **failure** |
  | review-pipeline-demo | Demo Pipeline | #1 | 35351409572 | success |
  | heziliu-pr-review-walkthrough | CI | #1 | 35409482531 | success |
  | ci-hygiene-demo | Smoke | #1 | 35262716626 | success |
  | log-retention-drill | smoke | #1 | 35261320289 | success |
  | release-automation-lab | Dispatch Smoke | #2 | 35422052222 | success |
  | pr-branch-demo | CI | #3 | 35289121268 | success |
- **Code scanning: BLOCKED on every org repo probed**, for two distinct reasons:
  - `403 Resource not accessible by personal access token` (token scope) — security-tracker, kg-triage-demo, github-automation-audit, agent-lab-notes, release-drill-lab, security-audit-2026, mcp-onboarding-brief, mcp-knowledge-base, aurora-migration (some of these return the second error).
  - `403 Advanced Security must be enabled for this repository to use code scanning` — aurora-migration, mcp-knowledge-base, actions-audit-2026.
  - No open code-scanning alert could be confirmed or ruled out anywhere with this token.
- Other repos with open issues tied to you (mcp-org-diligence, diabetes-trials-briefing, github-self-audit, workflow-demo-sandbox, kg-triage-demo, aurora-migration, ci-onboarding-demo, release-qa-rehearsal, mcp-onboarding-brief, mcp-knowledge-base, security-tracker): no workflows defined.

### CI failures worth knowing for planning (all completed, none running)
- agent-lab-notes — handoff-check run #4 (id 39309293682): failure; run recorded 0 jobs and its failed-job log endpoint returns nothing.
- security-audit-2026 — audit.yml run #4 (id 39275602362): failure; 0 jobs recorded, logs unavailable.
- pr-review-walkthrough-demo — ci.yml run #3 (id 35408464046): failure; 0 jobs recorded, logs 404.
- review-pipeline-demo — demo-ci run #2 (id 35237783176): failure; failed job `smoke` (`exit 1`).
- ci-postmortem-demo — demo-fail run #1 (id 35280949653): failure by design ("explode" job, `exit 1`), attempt 10.

## 3. Open PRs you authored

All have **pending** (not failing) checks: aurora-migration #5 "Add kickoff notes", ci-onboarding-demo #1 "Add project overview doc", release-qa-rehearsal #5 "docs: add release checklist", mcp-onboarding-brief #1 "Add onboarding brief for github-mcp-server", mcp-knowledge-base #1 "Add MCP onboarding brief".

*(A final "Actions taken" section is appended below once all checks and cancellations are complete.)*
