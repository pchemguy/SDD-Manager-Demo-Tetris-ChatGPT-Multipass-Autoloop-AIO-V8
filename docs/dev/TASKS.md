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
