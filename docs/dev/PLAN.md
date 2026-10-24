# Delivery plan

## Delivery strategy

Deliver bounded playable capabilities against the [SPEC](SPEC.md), preserving a usable game at each completed phase. Phase exits apply only to the explicit scope and contracts frozen in that phase, not the complete later product. The baseline uses its stated classic policies; a later increment may deliberately change defaults while retaining unrelated scoring, legal locking, restart and suspension guarantees.

Every implementation task includes its relevant tests and documentation. Every delivery milestone has a code-review/testing/report boundary; standalone review tasks follow the threshold stated in that milestone. The special phase review milestone always contains exactly one task and is excluded from delivery counts. Reports and HANDOFF are evidence, never substitutes for executing checks.

Implementation requires accepted preparation explicitly integrated and published to the actual default branch, then eligible-phase tracking activation. Provision browsers in isolation following BROWSER_DEV_POLICY; diagnose downloads/runtime failures proactively and preserve a blocked gate if required evidence remains unavailable. Chromium is primary, Firefox secondary; headless screenshots and interaction suffice. Tool versions are selected and pinned during implementation setup, not assumed installed here.

Only a complete authorized verified phase integrates. Publish every task commit before advancing; close/read back its issue, then milestones at their verified exits. Release each integrated phase with the listed version, root RELEASE-NOTES.md and matching GitHub tag/release. Capability increments use minor versions; fixes use patch versions.

## Phase 1 — Playable classic game

Outcome: A complete classic keyboard game with scoring, game over and restart. Target version: **0.1.0**. Depends on: accepted published preparation.

Included/excluded scope: Independent uniform sampling, collision-rejected clockwise rotation, failed-down locking, fixed gravity, soft drop and core browser UI. Enhancements, preview, bonuses and settings are excluded.

### Milestone 1.1 — Rules and verification foundation

Outcome and integration: Establish TypeScript tooling and isolated browser diagnostics; Implement board and tetromino geometry; Implement basic rotation and independent piece stream; Implement legal placement, row compaction and scoring.

Prerequisite: phase entry gate.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify B01–B06, B01, B01, B04, B03. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. A standalone review task follows the four delivery tasks.

### Milestone 1.2 — Playable session

Outcome and integration: Implement session spawn, gravity, lock and restart transitions; Render the board, score, status and restart control; Integrate keyboard repeat, event ordering and focus suspension.

Prerequisite: Milestone 1.1 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify B02–B05, B06, B02, B05. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 1.3 — Browser acceptance and distribution

Outcome and integration: Exercise complete classic sessions in both browsers; Verify desktop usability and input-control boundaries; Document and package the playable static build.

Prerequisite: Milestone 1.2 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify A01–A05, B06, A05. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 1.4 — Phase review

Exactly one phase code-review/testing/report task after every delivery milestone completes and closes. Assess B01–B06, A01–A05 against the included scope above, retained predecessor behavior except explicitly changed policies, documentation, reproducible static build and required browser evidence. Review code separately from test execution, repair all blockers, retain TODO disposition and refresh HANDOFF. Prepare release notes and version 0.1.0; explicitly integrate the verified complete phase, verify/publish the merged target, then tag and publish its GitHub release under the standing release instruction. Never release a partial or unverified phase.
