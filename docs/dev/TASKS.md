# Implementation tasks

The [PLAN](PLAN.md) owns strategic outcomes/exits, [SPEC](SPEC.md) owns behavior and [layout](layout.md) owns physical placement. Every task includes its relevant tests and documentation. All boxes are unimplemented work; document approval does not authorize execution. Select an implementation range separately after preparation integration and eligible-phase tracking. One task’s verified result, evidence and initial checkbox close in one commit, published/read back before advancing.

## Phase 1 — Playable classic game

- [ ] Phase 1 — Playable classic game
    - [ ] Milestone 1.1 — Rules and verification foundation
        - [ ] T-001 — Establish TypeScript tooling and isolated browser diagnostics
            Scope: package.json, tsconfig.json, vite.config.ts, playwright.config.ts; test harness. Depends on: accepted integrated preparation and verified phase activation.
            Contracts: B01–B06. Evidence: Run type/build and a minimal page smoke; provision Chromium/Firefox under the browser policy with concrete diagnostic evidence.
        - [ ] T-002 — Implement board and tetromino geometry
            Scope: src/domain/geometry.ts, board.ts; unit fixtures. Depends on: T-001.
            Contracts: B01. Evidence: Verify all seven masks, occupied-cell bounds, spawn cells and rejected overlap.
        - [ ] T-003 — Implement basic rotation and independent piece stream
            Scope: src/domain/geometry.ts, piece-stream.ts; unit tests. Depends on: T-002.
            Contracts: B01, B04. Evidence: Verify four rotations, O invariance, blocked rotation rejection and deterministic sample mapping.
        - [ ] T-004 — Implement legal placement, row compaction and scoring
            Scope: src/domain/board.ts, scoring.ts; unit tests. Depends on: T-003.
            Contracts: B03. Evidence: Verify exact cells, simultaneous row clears, retained row order, all scores and no partial writes.
        - [ ] T-005 — Review Milestone 1.1
            Depends on: T-001, T-002, T-003, T-004. Scope: whole milestone code review separately from checks, repair blockers, report and HANDOFF.
            Evidence: milestone exits and regressions verified; commit docs/dev/reports/phases/1/1.1.md and HANDOFF with this initial completion, then publish and close/read back the issue/milestone.
    - [ ] Milestone 1.2 — Playable session
        - [ ] T-006 — Implement session spawn, gravity, lock and restart transitions
            Scope: src/domain/session.ts; deterministic integration tests. Depends on: T-005.
            Contracts: B02–B05. Evidence: Trace fixed gravity/failed-down lock, blocked spawn, game over and full restart.
        - [ ] T-007 — Render the board, score, status and restart control
            Scope: src/browser/game-view.ts, styles.css, index.html; view tests. Depends on: T-006.
            Contracts: B06. Evidence: Inspect readable board/status and event-to-restart wiring without view-owned game rules.
        - [ ] T-008 — Integrate keyboard repeat, event ordering and focus suspension
            Scope: src/app/controller.ts, src/browser/main.ts; clock/input tests. Depends on: T-007.
            Contracts: B02, B05. Evidence: Exercise exact repeat/gravity ties, stale events, focus/visibility suspension and fresh resume anchors.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/1/1.2.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-006, T-007.
    - [ ] Milestone 1.3 — Browser acceptance and distribution
        - [ ] T-009 — Exercise complete classic sessions in both browsers
            Scope: tests/browser/classic.spec.ts and fixtures. Depends on: T-008.
            Contracts: A01–A05. Evidence: Interact with movement/rotation/drop, a line clear, top-out and restart in Chromium/Firefox; inspect screenshots.
        - [ ] T-010 — Verify desktop usability and input-control boundaries
            Scope: src/browser/game-view.ts, styles.css; browser tests. Depends on: T-009.
            Contracts: B06, A05. Evidence: Check 1280×800 fit, resizing state preservation, control labels/focus and page-scroll boundaries.
        - [ ] T-011 — Document and package the playable static build
            Scope: README.md, docs/user/CONTROLS.md, package scripts; dist verification. Depends on: T-010.
            Contracts: A01–A05. Evidence: Validate documented setup/build/preview commands against a clean install and built-page smoke; prepare baseline release evidence.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/1/1.3.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-009, T-010.
    - [ ] Milestone 1.4 — Phase review
        - [ ] T-012 — Review and report Phase 1
            Depends on: all Phase 1 delivery milestones completed and closed; final boundary T-011.
            Scope: code review, required tests, cross-milestone/browser regressions, blocker repair, phase exits and version 0.1.0 release preparation.
            Evidence: commit docs/dev/reports/phases/1/PHASE-REPORT.md and HANDOFF with this checkbox; include TODO dispositions, build/docs evidence and root release-note preparation. After publication and hosted closures, explicitly integrate, verify/publish merged default, then publish the required version tag and GitHub release. No next phase before these gates and actual continuation authority.

## Phase 2 — Enhanced piece handling

- [ ] Phase 2 — Enhanced piece handling
    - [ ] Milestone 2.1 — Sequence and Hold
        - [ ] T-013 — Implement deterministic seven-bag consumption
            Scope: src/domain/piece-stream.ts; unit tests. Depends on: T-012.
            Contracts: H01. Evidence: Verify each aligned bag permutation, refill and injected Fisher–Yates indices.
        - [ ] T-014 — Implement Hold as a session transaction
            Scope: src/domain/session.ts; unit/integration tests. Depends on: T-013.
            Contracts: H01. Evidence: Verify once-per-piece, empty consumption, swap non-consumption, reset timing and failed-spawn top-out.
        - [ ] T-015 — Integrate Hold controls and held-piece display
            Scope: src/browser/game-view.ts, src/app/controller.ts; browser tests. Depends on: T-014.
            Contracts: H01, A06. Evidence: C/Shift edges, ignored repeats and display agree with session state through restart.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/2/2.1.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-013, T-014.
    - [ ] Milestone 2.2 — Rotation and landing controls
        - [ ] T-016 — Implement ordered clockwise wall kicks
            Scope: src/domain/geometry.ts, session.ts; kick fixtures. Depends on: T-015.
            Contracts: H02. Evidence: Choose first legal candidate across walls/floor/stack; reject unchanged when all fail.
        - [ ] T-017 — Implement shared normal landing and ghost rendering
            Scope: src/domain/landing.ts, src/browser/game-view.ts; fixtures. Depends on: T-016.
            Contracts: H02, A07. Evidence: Ghost cells match consecutive legal descent; view has no independent collision solver.
        - [ ] T-018 — Integrate edge-triggered hard drop
            Scope: src/domain/session.ts, src/app/controller.ts; browser fixtures. Depends on: T-017.
            Contracts: H03. Evidence: Space reaches exact projected cells without board writes, repeat score or forced immediate lock.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/2/2.2.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-016, T-017.
    - [ ] Milestone 2.3 — Contact timing and regression
        - [ ] T-019 — Implement full grounded-interval locking
            Scope: src/domain/session.ts; clock fixtures. Depends on: T-018.
            Contracts: H04, A08. Evidence: Verify first-contact deadline, no grounded reset, cancellation airborne and fresh re-grounding.
        - [ ] T-020 — Integrate contact deadlines with input and Hold
            Scope: src/app/controller.ts, src/domain/session.ts; integration tests. Depends on: T-019.
            Contracts: B05, H01, H03–H04. Evidence: Verify simultaneous deadlines, zero-distance hard drop, suspended contact and discarded held-piece events.
        - [ ] T-021 — Verify and document enhanced browser gameplay
            Scope: tests/browser/enhanced.spec.ts, docs/user/CONTROLS.md, README.md. Depends on: T-020.
            Contracts: A06–A09. Evidence: Check both browsers, ghost/drop agreement, Hold, kicks, contact time and retained classic scoring/top-out/restart; prepare release evidence.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/2/2.3.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-019, T-020.
    - [ ] Milestone 2.4 — Phase review
        - [ ] T-022 — Review and report Phase 2
            Depends on: all Phase 2 delivery milestones completed and closed; final boundary T-021.
            Scope: code review, required tests, cross-milestone/browser regressions, blocker repair, phase exits and version 0.2.0 release preparation.
            Evidence: commit docs/dev/reports/phases/2/PHASE-REPORT.md and HANDOFF with this checkbox; include TODO dispositions, build/docs evidence and root release-note preparation. After publication and hosted closures, explicitly integrate, verify/publish merged default, then publish the required version tag and GitHub release. No next phase before these gates and actual continuation authority.

## Phase 3 — Dynamic ghost visibility

- [ ] Phase 3 — Dynamic ghost visibility
    - [ ] Milestone 3.1 — Midline-aware ghost
        - [ ] T-023 — Implement occupied-cell midline classification
            Scope: src/domain/ghost-visibility.ts; unit fixtures. Depends on: T-022.
            Contracts: G01. Evidence: Highest projected row 9 hides, row 10/11 shows; tall straddling shapes hide.
        - [ ] T-024 — Integrate dynamic visibility without landing side effects
            Scope: src/browser/game-view.ts; application tests. Depends on: T-023.
            Contracts: G01, A10. Evidence: Moves/rotations show/hide in both directions while drop target and deadlines remain identical.
        - [ ] T-025 — Verify and document dynamic ghost behavior
            Scope: tests/browser/ghost.spec.ts, docs/user/CONTROLS.md. Depends on: T-024.
            Contracts: A10. Evidence: Inspect representative Chromium/Firefox transitions/screenshots and retained hard-drop timing; prepare release evidence.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/3/3.1.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-023, T-024.
    - [ ] Milestone 3.2 — Phase review
        - [ ] T-026 — Review and report Phase 3
            Depends on: all Phase 3 delivery milestones completed and closed; final boundary T-025.
            Scope: code review, required tests, cross-milestone/browser regressions, blocker repair, phase exits and version 0.3.0 release preparation.
            Evidence: commit docs/dev/reports/phases/3/PHASE-REPORT.md and HANDOFF with this checkbox; include TODO dispositions, build/docs evidence and root release-note preparation. After publication and hosted closures, explicitly integrate, verify/publish merged default, then publish the required version tag and GitHub release. No next phase before these gates and actual continuation authority.

## Phase 4 — Penetrator gameplay

- [ ] Phase 4 — Penetrator gameplay
    - [ ] Milestone 4.1 — Traversal and active-piece lifecycle
        - [ ] T-027 — Implement mode-aware terminal landing search
            Scope: src/domain/landing.ts; adversarial board fixtures. Depends on: T-026.
            Contracts: P02, A11. Evidence: Scan below intervening blockers; prove sealed cavities, target above floor and absent candidate target.
        - [ ] T-028 — Integrate penetrator descent and legal contact
            Scope: src/domain/session.ts, geometry.ts; timing tests. Depends on: T-027.
            Contracts: P02–P03. Evidence: Gravity/soft/hard drop reach the same legal target; overlapping intermediate states never lock or alter settled cells.
        - [ ] T-029 — Implement atomic activation and active Hold exclusion
            Scope: src/domain/session.ts, src/app/controller.ts; tests. Depends on: T-028.
            Contracts: P01–P03. Evidence: P spends once only when eligible; candidate rejection, repeated activation, Hold rejection and contact recomputation preserve invariants.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/4/4.1.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-027, T-028.
    - [ ] Milestone 4.2 — Rewards, indicators and acceptance
        - [ ] T-030 — Award capped bonuses in the lock transaction
            Scope: src/domain/session.ts; lock/clear fixtures. Depends on: T-029.
            Contracts: P01, P03. Evidence: Four lines award one up to three, other clears none; restart begins at zero.
        - [ ] T-031 — Render white active ability and live bonus indicators
            Scope: src/browser/game-view.ts, styles.css; view tests. Depends on: T-030.
            Contracts: P01. Evidence: Four active cells white, regular/settled kinds non-white, ghost distinct; one lightning symbol per bonus and accessible count.
        - [ ] T-032 — Verify penetrator interactions and document controls
            Scope: tests/browser/penetrator.spec.ts, docs/user/CONTROLS.md. Depends on: T-031.
            Contracts: A11–A12. Evidence: Both browsers exercise earned/spent/capped inventory, traversal, ghost/drop agreement, active Hold rejection, legal locks and restart; prepare release evidence.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/4/4.2.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-030, T-031.
    - [ ] Milestone 4.3 — Phase review
        - [ ] T-033 — Review and report Phase 4
            Depends on: all Phase 4 delivery milestones completed and closed; final boundary T-032.
            Scope: code review, required tests, cross-milestone/browser regressions, blocker repair, phase exits and version 0.4.0 release preparation.
            Evidence: commit docs/dev/reports/phases/4/PHASE-REPORT.md and HANDOFF with this checkbox; include TODO dispositions, build/docs evidence and root release-note preparation. After publication and hosted closures, explicitly integrate, verify/publish merged default, then publish the required version tag and GitHub release. No next phase before these gates and actual continuation authority.

## Phase 5 — Session game configuration

- [ ] Phase 5 — Session game configuration
    - [ ] Milestone 5.1 — Configuration and controls
        - [ ] T-034 — Implement typed session settings and defaults
            Scope: src/app/configuration.ts; model tests. Depends on: T-033.
            Contracts: C01. Evidence: Validate six finite value domains/defaults and preserve selected values across Restart.
        - [ ] T-035 — Render six labeled side-panel controls
            Scope: src/browser/settings-view.ts, styles.css; browser tests. Depends on: T-034.
            Contracts: C01, A13. Evidence: Keyboard changes reach Configuration; controls show selected values and do not trigger gameplay keys.
        - [ ] T-036 — Add non-consuming next preview and ghost display modes
            Scope: src/browser/settings-view.ts, game-view.ts, src/domain/piece-stream.ts; tests. Depends on: T-035.
            Contracts: C01–C02. Evidence: Peek never consumes a bag entry; hide/dynamic/show and preview on/off render exact state.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/5/5.1.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-034, T-035.
    - [ ] Milestone 5.2 — Live application and session acceptance
        - [ ] T-037 — Snapshot timing policies for each active piece
            Scope: src/domain/session.ts, src/app/configuration.ts; time tests. Depends on: T-036.
            Contracts: C02, A14. Evidence: Current timer unchanged on selection; next spawn/Hold/Restart snapshots policies and pending display clears.
        - [ ] T-038 — Apply enable flags and failed/immediate locking
            Scope: src/app/controller.ts, src/domain/session.ts, settings-view.ts; tests. Depends on: T-037.
            Contracts: C02. Evidence: Disabled commands no-op; Hold retains kind; failed-down/general drop and immediate legal drop match contracts, including penetrators.
        - [ ] T-039 — Verify session configuration and document semantics
            Scope: tests/browser/configuration.spec.ts, docs/user/SETTINGS.md, README.md. Depends on: T-038.
            Contracts: A13–A15. Evidence: Both browsers exercise every option, pending-policy timing, Restart retention and reload-to-default without storage/URL effects; prepare release evidence.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/5/5.2.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-037, T-038.
    - [ ] Milestone 5.3 — Phase review
        - [ ] T-040 — Review and report Phase 5
            Depends on: all Phase 5 delivery milestones completed and closed; final boundary T-039.
            Scope: code review, required tests, cross-milestone/browser regressions, blocker repair, phase exits and version 0.5.0 release preparation.
            Evidence: commit docs/dev/reports/phases/5/PHASE-REPORT.md and HANDOFF with this checkbox; include TODO dispositions, build/docs evidence and root release-note preparation. After publication and hosted closures, explicitly integrate, verify/publish merged default, then publish the required version tag and GitHub release. No next phase before these gates and actual continuation authority.

## Phase 6 — Persistent configuration

- [ ] Phase 6 — Persistent configuration
    - [ ] Milestone 6.1 — Source resolution and initialization
        - [ ] T-041 — Implement finite settings codecs and candidate parsing
            Scope: src/browser/settings-persistence.ts, src/app/configuration.ts; fixtures. Depends on: T-040.
            Contracts: S01. Evidence: Exact tokens, empty/wrong-case/malformed/duplicate candidates stay isolated per setting.
        - [ ] T-042 — Resolve URL, cookie and default values independently
            Scope: src/browser/settings-persistence.ts, src/browser/main.ts; integration tests. Depends on: T-041.
            Contracts: S01–S02. Evidence: Mixed-source precedence resolves before first piece; omission retains cookie; valid explicit defaults write cookies.
        - [ ] T-043 — Integrate cookie lifetime and initialization failure status
            Scope: src/browser/settings-persistence.ts, settings-view.ts; adapter tests. Depends on: T-042.
            Contracts: S02–S03. Evidence: Use specified cookie attributes, guarded reads/writes and non-blocking warning without erasing other values.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/6/6.1.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-041, T-042.
    - [ ] Milestone 6.2 — Synchronization and reload acceptance
        - [ ] T-044 — Synchronize selected changes to cookies and URL
            Scope: src/browser/settings-persistence.ts, src/app/controller.ts; fixtures. Depends on: T-043.
            Contracts: S02. Evidence: Replace only selected key, remove its duplicates, preserve unrelated params/fragment/path and avoid navigation.
        - [ ] T-045 — Contain partial persistence failures
            Scope: src/browser/settings-persistence.ts, settings-view.ts; failure tests. Depends on: T-044.
            Contracts: S03. Evidence: Cookie and History fail separately; other channel attempted, memory remains effective and warnings truthful.
        - [ ] T-046 — Verify real-browser reload persistence and document settings
            Scope: tests/browser/persistence.spec.ts, docs/user/SETTINGS.md, README.md. Depends on: T-045.
            Contracts: A16–A18. Evidence: HTTP(S) Chromium/Firefox mixed-source, explicit-default, omitted-key, change/reload, invalid-input and failure checks; prepare release evidence.
            Milestone boundary: after all other milestone tasks, review the whole capability code separately from tests, run applicable regressions and repair blockers; commit docs/dev/reports/phases/6/6.2.md and HANDOFF with this task’s result and initial checkbox. Publish/read back, then close/read back issue/milestone. Depends additionally on: T-044, T-045.
    - [ ] Milestone 6.3 — Phase review
        - [ ] T-047 — Review and report Phase 6
            Depends on: all Phase 6 delivery milestones completed and closed; final boundary T-046.
            Scope: code review, required tests, cross-milestone/browser regressions, blocker repair, phase exits and version 0.6.0 release preparation.
            Evidence: commit docs/dev/reports/phases/6/PHASE-REPORT.md and HANDOFF with this checkbox; include TODO dispositions, build/docs evidence and root release-note preparation. Also aggregate all unresolved/deferred findings in docs/dev/reports/IMPLEMENTATION-REPORT.md when the full list is complete. After publication and hosted closures, explicitly integrate, verify/publish merged default, then publish the required version tag and GitHub release. No next phase before these gates and actual continuation authority.
