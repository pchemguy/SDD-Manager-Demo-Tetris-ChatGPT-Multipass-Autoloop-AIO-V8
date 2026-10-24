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
