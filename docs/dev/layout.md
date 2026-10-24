# Repository layout

## Status and ownership

Source, test, tooling, user-document and distribution paths below are planned allocations, not claims that code exists. Existing root policies, bundled skills and development records remain at their current paths. This map realizes [DECOMPOSITION](DECOMPOSITION.md) and the delivery route in [PLAN](PLAN.md).

| Area | Physical owner / intended paths | Boundary | Checks / fixtures |
| --- | --- | --- | --- |
| Domain values and rules | src/domain/types.ts, geometry.ts, board.ts, scoring.ts, piece-stream.ts, session.ts | Pure game state/transitions; no DOM/time/storage globals. | tests/unit/, tests/integration/ |
| Application orchestration | src/app/controller.ts | Input sequencing, elapsed simulation time and suspension. | tests/integration/ controller/clock fixtures |
| Browser presentation/bootstrap | src/browser/main.ts, game-view.ts, styles.css; index.html | Composition, key/lifecycle adapters, Canvas and HTML. | tests/browser/ with isolated fixtures |
| Build and checks | package.json, lockfile, tsconfig.json, vite.config.ts, playwright.config.ts | Pinned dev dependencies, build and isolated browser projects. | Type/build and browser setup diagnostics |
| Documentation and distribution | README.md, docs/user/CONTROLS.md; dist/ (generated) | Validated user/developer commands, controls, static build. | Built-page smoke and documented command readback |
| Landing and enhanced controls | src/domain/landing.ts; existing session/stream/controller/view modules | Canonical landing, bag/Hold and timing remain with their logical owners. | tests/unit/ landing/bag/kick; tests/browser/enhanced.spec.ts |
| Ghost visibility | src/domain/ghost-visibility.ts | Pure occupied-cell predicate; browser view renders it. | tests/unit/ midline fixtures; tests/browser/ghost.spec.ts |
| Penetrator behavior | Existing landing.ts, geometry.ts, session.ts, controller.ts and game-view.ts | Mode/inventory rules stay in session; landing module owns both modes. | tests/unit/ cavity fixtures; tests/browser/penetrator.spec.ts |
| Configuration and settings UI | src/app/configuration.ts; src/browser/settings-view.ts; docs/user/SETTINGS.md | Validated selected state vs per-piece snapshots; ordinary HTML controls. | tests/unit/ settings; tests/browser/configuration.spec.ts |

## Shared paths and generated artifacts

Keep test board/sequence/clock fixtures under tests/fixtures/ and browser-run artifacts under ignored test-results/ and playwright-report/. Browser binaries belong to a dedicated isolated cache outside committed source, following the root browser policy. Do not modify /pyenv. Build output dist/ and dependencies node_modules/ are generated and ignored; the implementation setup task establishes actual ignore rules and scripts.

Development roots and their adjacent review reports live in docs/dev/. Main implementation milestone reports use docs/dev/reports/phases/<phase-id>/<milestone-id>.md; phase reports use PHASE-REPORT.md in that phase directory; the final aggregate is docs/dev/reports/IMPLEMENTATION-REPORT.md. RELEASE-NOTES.md is the root release body when a release is authorized. These report/output paths are reserved, not existing-link claims.

Only the browser boundary imports browser globals. Domain types and helpers have a single owner; application/view consumers import their contracts. Put component tests at the appropriate unit/integration/browser layer and avoid duplicating every case at every layer. Package tooling owns build/check declarations; README documents only validated commands. Root AGENTS navigation points to current governing documents and does not claim unrun commands work.
