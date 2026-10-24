# SPEC review report

## Current gate

State: **Ready** for the reviewed document scope. Current identities and criteria are in the latest review section below. Human acceptance/preapproval is retained separately in DOCS_PREPARATION.

## Initial review

Scope: cumulative product state through Playable classic baseline; owner conformance review.

- SPEC.md: SHA-256 `aef8d2b6aeeaeae45493f2bc5acccb00bef42b4b39efd248df9509d96f7cae98`.
- PROJECT.md: SHA-256 `e7cbdb66fe1b201a43f30235956314927b54636c7076e6da227f488faf46797e`.
- ARCHITECTURE.md: SHA-256 `9fa5316a28699356b8cdb67dbec75c8cf4de9b82798c5c501a6e4d13bb835849`.
- DECOMPOSITION.md: SHA-256 `f5370d6ef03258bdd1568ca269ed538b9c39090aed2e0de44bfdabb7b0969037`.

Geometry/movement/transactions → Geometry, Board, GameSession; input/time/suspension → GameController; rendering/status → GameView. End-to-end success, rejection, timing, restart and browser acceptance map to the named owners. No contract requires a hidden browser-global dependency in the domain.

Checks: semantic comparison against the governing roots, ownership/dependency and acceptance mapping, current-scope exclusions, relative links and Markdown spacing. No unresolved confirmed finding. Readiness is limited to document conformance; runtime/browser behavior, installation, implementation acceptance and whole-package DOCS-009 QC have not run.

## Revision 1

Scope: cumulative product state through Playable classic baseline; owner conformance review.

- SPEC.md: SHA-256 `970e3da5659435e04f4cdb8c055cbfeb47af3a1191bc9d268185e1fec68c4c7f`.
- PROJECT.md: SHA-256 `e7cbdb66fe1b201a43f30235956314927b54636c7076e6da227f488faf46797e`.
- ARCHITECTURE.md: SHA-256 `9fa5316a28699356b8cdb67dbec75c8cf4de9b82798c5c501a6e4d13bb835849`.
- DECOMPOSITION.md: SHA-256 `f5370d6ef03258bdd1568ca269ed538b9c39090aed2e0de44bfdabb7b0969037`.

Geometry/movement/transactions → Geometry, Board, GameSession; input/time/suspension → GameController; rendering/status → GameView. End-to-end success, rejection, timing, restart and browser acceptance map to the named owners. No contract requires a hidden browser-global dependency in the domain.

Checks: semantic comparison against the governing roots, ownership/dependency and acceptance mapping, current-scope exclusions, relative links and Markdown spacing. No unresolved confirmed finding. Readiness is limited to document conformance; runtime/browser behavior, installation, implementation acceptance and whole-package DOCS-009 QC have not run.

## Revision 2

Scope: cumulative product state through Gameplay enhancements; owner conformance review.

- SPEC.md: SHA-256 `4a71fc23fe2bfb986ff51348eb4f6e2e30991aa59fcf281b2482ec7a2b1b6c0d`.
- PROJECT.md: SHA-256 `43d3867f365f0e2e0d73e11915d612fb0582874095e849e19c915671c3566320`.
- ARCHITECTURE.md: SHA-256 `044eee949727cb52ab9b3c913da77c319bb38d67f1cc4991f4d082dd92d55a90`.
- DECOMPOSITION.md: SHA-256 `64266f02aa79df66efa4301ece6133bfd75db139419a3b8853d2b8cdc227971e`.

Geometry/movement/transactions → Geometry, Board, GameSession; input/time/suspension → GameController; rendering/status → GameView. H01–H04 → PieceStream, LandingSolver and contact/Hold lifecycle; End-to-end success, rejection, timing, restart and browser acceptance map to the named owners. No contract requires a hidden browser-global dependency in the domain.

Checks: semantic comparison against the governing roots, ownership/dependency and acceptance mapping, current-scope exclusions, relative links and Markdown spacing. No unresolved confirmed finding. Readiness is limited to document conformance; runtime/browser behavior, installation, implementation acceptance and whole-package DOCS-009 QC have not run.

## Revision 3

Scope: cumulative product state through Conditional ghost visibility; owner conformance review.

- SPEC.md: SHA-256 `959dd151792880656c0bb6cc19c0ec1567000679b2fa715d54590ff9fdceccbb`.
- PROJECT.md: SHA-256 `896f8c8ec6548ebb1b6c677ce2a0fe7dad7715c6a19063493227a51269781f87`.
- ARCHITECTURE.md: SHA-256 `57f71a70e3d48982fdd2804e44feef8e3e5d4113f31148e989ca75d8288af324`.
- DECOMPOSITION.md: SHA-256 `8bab4a2726e8c99bd243361b9653c0c9022597a23772ea1530bac74a1b72b6d0`.

Geometry/movement/transactions → Geometry, Board, GameSession; input/time/suspension → GameController; rendering/status → GameView. H01–H04 → PieceStream, LandingSolver and contact/Hold lifecycle; G01 → GhostVisibility; End-to-end success, rejection, timing, restart and browser acceptance map to the named owners. No contract requires a hidden browser-global dependency in the domain.

Checks: semantic comparison against the governing roots, ownership/dependency and acceptance mapping, current-scope exclusions, relative links and Markdown spacing. No unresolved confirmed finding. Readiness is limited to document conformance; runtime/browser behavior, installation, implementation acceptance and whole-package DOCS-009 QC have not run.

## Revision 4

Scope: cumulative product state through Penetrator mode; owner conformance review.

- SPEC.md: SHA-256 `df64660f8bc63042f389bcefc611fdb046c65f0e1ee6f4ace0bdb807e351b806`.
- PROJECT.md: SHA-256 `0223212f979446e67e70b1421a4c04d2a162d4b72d3f0e8a08992768dda2257a`.
- ARCHITECTURE.md: SHA-256 `f7cf1ee36b42645eb9456be243edf2887eaa5d2b4b6f110a64eae6de3acbeedc`.
- DECOMPOSITION.md: SHA-256 `de2ce7c73c91a3e363d224a1f6f27126a7846be56b8be1eb986ec112e2c3cf26`.

Geometry/movement/transactions → Geometry, Board, GameSession; input/time/suspension → GameController; rendering/status → GameView. H01–H04 → PieceStream, LandingSolver and contact/Hold lifecycle; G01 → GhostVisibility; P01–P03 → mode-aware solver/session inventory and legal Board transaction; End-to-end success, rejection, timing, restart and browser acceptance map to the named owners. No contract requires a hidden browser-global dependency in the domain.

Checks: semantic comparison against the governing roots, ownership/dependency and acceptance mapping, current-scope exclusions, relative links and Markdown spacing. No unresolved confirmed finding. Readiness is limited to document conformance; runtime/browser behavior, installation, implementation acceptance and whole-package DOCS-009 QC have not run.

### Finding SPEC-F01 — Rejection versus locking

Earlier B02/A01 generic rejection wording could include a blocked downward attempt even though B04 allows that attempt to lock; command timing wording could also include replacement by Hold. sdd-specify qualified lateral/rotation rejection and current-piece gravity scheduling, preserving the explicit downward locking and new-piece timing contracts. Recheck: failed down can legally write a lock; rejected lateral/rotation candidates cannot. Disposition: resolved without changing protected phase/task scope.

### Finding SPEC-F02 — Active color exception

B06 broadly described non-white current pieces; P01 requires white active penetrators. sdd-specify explicitly limits B06 to regular cells and routes active ability color to P01. Recheck: regular/settled cells remain non-white, active penetrators white. Disposition: resolved.

## Revision 5

Scope: cumulative product state through Session-only game configuration; owner conformance review.

- SPEC.md: SHA-256 `97b963da55c419e0aa94a4b795a81dd85ca76de8e7c3e8490ae802e243af3c14`.
- PROJECT.md: SHA-256 `344b922dfd4ce1e3384ae907270a2b6cb20b4cd33bee5aba9acde7c9a0250341`.
- ARCHITECTURE.md: SHA-256 `35e5e1c278d382db28b0e45bbcb9db5236b6a7a4f1ef81e84352e274855bda20`.
- DECOMPOSITION.md: SHA-256 `7e13dfc5e265dd4d8800136e519ba5336dd5e4a276eb18e17830979863798a22`.

Geometry/movement/transactions → Geometry, Board, GameSession; input/time/suspension → GameController; rendering/status → GameView. H01–H04 → PieceStream, LandingSolver and contact/Hold lifecycle; G01 → GhostVisibility; P01–P03 → mode-aware solver/session inventory and legal Board transaction; C01–C02 → Configuration and SettingsView; End-to-end success, rejection, timing, restart and browser acceptance map to the named owners. No contract requires a hidden browser-global dependency in the domain.

Checks: semantic comparison against the governing roots, ownership/dependency and acceptance mapping, current-scope exclusions, relative links and Markdown spacing. No unresolved confirmed finding. Readiness is limited to document conformance; runtime/browser behavior, installation, implementation acceptance and whole-package DOCS-009 QC have not run.
