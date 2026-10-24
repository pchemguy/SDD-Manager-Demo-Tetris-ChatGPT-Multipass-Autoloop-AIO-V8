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

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify B01 geometry, B03 placement/compaction/scoring (excluding next-spawn integration), B04 rotation and independent sampling, and B06 browser provisioning only. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. A standalone review task follows the four delivery tasks.

### Milestone 1.2 — Playable session

Outcome and integration: Implement session spawn, gravity, lock and restart transitions; Render the board, score, status and restart control; Integrate keyboard repeat, event ordering and focus suspension.

Prerequisite: Milestone 1.1 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify B02 session/input/gravity, B03 lock-to-spawn integration, B04 failed-down locking, B05 ordering/suspension and B06 core view. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 1.3 — Browser acceptance and distribution

Outcome and integration: Exercise complete classic sessions in both browsers; Verify desktop usability and input-control boundaries; Document and package the playable static build.

Prerequisite: Milestone 1.2 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify B06 desktop usability and A01–A05 integrated classic acceptance. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 1.4 — Phase review

Exactly one phase code-review/testing/report task after every delivery milestone completes and closes. Assess B01–B06, A01–A05 against the included scope above, retained predecessor behavior except explicitly changed policies, documentation, reproducible static build and required browser evidence. Review code separately from test execution, repair all blockers, retain TODO disposition and refresh HANDOFF. Prepare release notes and version 0.1.0; explicitly integrate the verified complete phase, verify/publish the merged target, then tag and publish its GitHub release under the standing release instruction. Never release a partial or unverified phase.

## Phase 2 — Enhanced piece handling

Outcome: Modern piece handling with predictable sequence, Hold, kicks, ghost, hard drop and contact delay. Target version: **0.2.0**. Depends on: completed, verified, integrated and released Phase 1.

Included/excluded scope: Implement enhanced policies together because Hold, landing and contact timing share active-piece lifecycle. Conditional ghost hiding, penetrator, next preview and settings are excluded.

### Milestone 2.1 — Sequence and Hold

Outcome and integration: Implement deterministic seven-bag consumption; Implement Hold as a session transaction; Integrate Hold controls and held-piece display.

Prerequisite: phase entry gate.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify H01, H01, A06. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 2.2 — Rotation and landing controls

Outcome and integration: Implement ordered clockwise wall kicks; Implement shared normal landing and ghost rendering; Integrate edge-triggered hard drop.

Prerequisite: Milestone 2.1 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify H02 kick/landing behavior and H03 hard-drop placement/input only; full grounded-delay acceptance belongs to Milestone 2.3. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 2.3 — Contact timing and regression

Outcome and integration: Implement full grounded-interval locking; Integrate contact deadlines with input and Hold; Verify and document enhanced browser gameplay.

Prerequisite: Milestone 2.2 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify H04, A08, B05, H01, H03–H04, A06–A09. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 2.4 — Phase review

Exactly one phase code-review/testing/report task after every delivery milestone completes and closes. Assess H01–H04, A06–A09 against the included scope above, retained predecessor behavior except explicitly changed policies, documentation, reproducible static build and required browser evidence. Review code separately from test execution, repair all blockers, retain TODO disposition and refresh HANDOFF. Prepare release notes and version 0.2.0; explicitly integrate the verified complete phase, verify/publish the merged target, then tag and publish its GitHub release under the standing release instruction. Never release a partial or unverified phase.

## Phase 3 — Dynamic ghost visibility

Outcome: The ghost responds to the projected piece’s occupied-cell position relative to the midline. Target version: **0.3.0**. Depends on: completed, verified, integrated and released Phase 2.

Included/excluded scope: Only conditional rendering and its direct regressions; no configuration UI or change to the target solver.

### Milestone 3.1 — Midline-aware ghost

Outcome and integration: Implement occupied-cell midline classification; Integrate dynamic visibility without landing side effects; Verify and document dynamic ghost behavior.

Prerequisite: phase entry gate.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify G01, G01, A10, A10. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 3.2 — Phase review

Exactly one phase code-review/testing/report task after every delivery milestone completes and closes. Assess G01, A10 against the included scope above, retained predecessor behavior except explicitly changed policies, documentation, reproducible static build and required browser evidence. Review code separately from test execution, repair all blockers, retain TODO disposition and refresh HANDOFF. Prepare release notes and version 0.3.0; explicitly integrate the verified complete phase, verify/publish the merged target, then tag and publish its GitHub release under the standing release instruction. Never release a partial or unverified phase.

## Phase 4 — Penetrator gameplay

Outcome: A limited earned ability traverses stacks and lands legally in the lowest cavity. Target version: **0.4.0**. Depends on: completed, verified, integrated and released Phase 3.

Included/excluded scope: Mode-aware descent/rotation, activation/Hold exclusion, bonuses and white visual status. Configuration and persistent state are excluded.

### Milestone 4.1 — Traversal and active-piece lifecycle

Outcome and integration: Implement mode-aware terminal landing search; Integrate penetrator descent and legal contact; Implement atomic activation and active Hold exclusion.

Prerequisite: phase entry gate.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify P01 activation and Hold exclusion, P02 traversal/terminal search, and P03 legal locking; earned rewards/indicator acceptance belongs to Milestone 4.2. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 4.2 — Rewards, indicators and acceptance

Outcome and integration: Award capped bonuses in the lock transaction; Render white active ability and live bonus indicators; Verify penetrator interactions and document controls.

Prerequisite: Milestone 4.1 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify P01–P03 complete reward/visual/gameplay integration and A11–A12. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 4.3 — Phase review

Exactly one phase code-review/testing/report task after every delivery milestone completes and closes. Assess P01–P03, A11–A12 against the included scope above, retained predecessor behavior except explicitly changed policies, documentation, reproducible static build and required browser evidence. Review code separately from test execution, repair all blockers, retain TODO disposition and refresh HANDOFF. Prepare release notes and version 0.4.0; explicitly integrate the verified complete phase, verify/publish the merged target, then tag and publish its GitHub release under the standing release instruction. Never release a partial or unverified phase.

## Phase 5 — Session game configuration

Outcome: Six side-panel settings control gameplay within the current page session. Target version: **0.5.0**. Depends on: completed, verified, integrated and released Phase 4.

Included/excluded scope: Settings controls/defaults, next preview and safe live changes; no cookies, URL access or cross-reload persistence.

### Milestone 5.1 — Configuration and controls

Outcome and integration: Implement typed session settings and defaults; Render six labeled side-panel controls; Add non-consuming next preview and ghost display modes.

Prerequisite: phase entry gate.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify C01 selected values/defaults/controls and C02 ghost/preview display; timing-policy/enable integration belongs to Milestone 5.2. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 5.2 — Live application and session acceptance

Outcome and integration: Snapshot timing policies for each active piece; Apply enable flags and failed/immediate locking; Verify session configuration and document semantics.

Prerequisite: Milestone 5.1 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify C01–C02 complete live behavior and A13–A15. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 5.3 — Phase review

Exactly one phase code-review/testing/report task after every delivery milestone completes and closes. Assess C01–C02, A13–A15 against the included scope above, retained predecessor behavior except explicitly changed policies, documentation, reproducible static build and required browser evidence. Review code separately from test execution, repair all blockers, retain TODO disposition and refresh HANDOFF. Prepare release notes and version 0.5.0; explicitly integrate the verified complete phase, verify/publish the merged target, then tag and publish its GitHub release under the standing release instruction. Never release a partial or unverified phase.

## Phase 6 — Persistent configuration

Outcome: URL and cookies restore each setting independently without disrupting gameplay. Target version: **0.6.0**. Depends on: completed, verified, integrated and released Phase 5.

Included/excluded scope: Configuration serialization, precedence, writes and guarded failures only; no board/game-state persistence or new gameplay features.

### Milestone 6.1 — Source resolution and initialization

Outcome and integration: Implement finite settings codecs and candidate parsing; Resolve URL, cookie and default values independently; Integrate cookie lifetime and initialization failure status.

Prerequisite: phase entry gate.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify S01 source resolution, S02 cookie initialization and S03 guarded cookie status; History-change synchronization belongs to Milestone 6.2. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 6.2 — Synchronization and reload acceptance

Outcome and integration: Synchronize selected changes to cookies and URL; Contain partial persistence failures; Verify real-browser reload persistence and document settings.

Prerequisite: Milestone 6.1 completion and closure.

Exit: demonstrate the integrated capability to inform continue/amend/simplify/stop; verify S01–S03 complete synchronization/failure handling and A16–A18. Whole-capability code review, applicable regression checks, blocker repairs, a committed milestone report and HANDOFF are required. The final delivery task owns the review/report/HANDOFF boundary; no standalone milestone review task.

### Milestone 6.3 — Phase review

Exactly one phase code-review/testing/report task after every delivery milestone completes and closes. Assess S01–S03, A16–A18 against the included scope above, retained predecessor behavior except explicitly changed policies, documentation, reproducible static build and required browser evidence. Review code separately from test execution, repair all blockers, retain TODO disposition and refresh HANDOFF. Include final implementation-report/TODO aggregation when this phase is the authorized full-list completion. Prepare release notes and version 0.6.0; explicitly integrate the verified complete phase, verify/publish the merged target, then tag and publish its GitHub release under the standing release instruction. Never release a partial or unverified phase.
