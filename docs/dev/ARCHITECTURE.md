# Architecture

## Context and arrangement

The [project brief](PROJECT.md) defines a static keyboard game. Three blocks separate decisions that change for different reasons: a deterministic game domain, application orchestration and a browser presentation/platform boundary. TypeScript module exports are sufficient; no framework, dependency-injection container or inheritance hierarchy is required.

| Block | Owns | Depends on |
| --- | --- | --- |
| Game domain | Board, piece geometry, movement/locking, line/score transactions, session state and pure transitions | Domain values and explicit randomness/time inputs only |
| Application | Ordered command dispatch, simulation-time advancement, focus suspension and coherent snapshots | Domain operations; narrow browser-facing ports |
| Browser shell | Canvas/HTML rendering, key events, focus/lifecycle events and monotonic-clock sampling | Application commands and read-only snapshots |

Browser events flow inward as commands; snapshots flow outward. The browser shell never mutates board arrays. The domain imports no DOM, timers, cookies or URL globals. Only the application translates browser time to simulation time. Rendering is derived from a snapshot and cannot advance the game.

## State and transactions

The game session is the authoritative owner of settled board cells, active piece, score and playing/game-over status. Geometry helpers and board queries remain pure. Random values and elapsed time are explicit inputs; production adapters and deterministic fixtures share the same contracts. Lock, completed-row removal, scoring and next spawn form one atomic transition, so observers never see half-cleared boards or two active pieces.

- The domain owns piece-stream state, held piece, landing projection and lock/contact state. One projection feeds ghost display and hard drop; neither renderer nor keyboard code duplicates collision logic.
- Visibility is a projection predicate, separate from solving the landing. Hiding the ghost never changes the drop target.

## Timing and failure boundaries

Simulation time advances only while the document is visible and focused. The application clears held-key state on suspension and resumes from a fresh browser-clock anchor. Input order is serialized; no event listener changes game state during rendering. Invalid or unavailable gameplay commands are no-ops, while an impossible next spawn is a normal game-over outcome. Browser setup/build errors are development failures rather than in-game states.

## Rationale and seams

Canvas keeps board rendering compact; HTML provides ordinary controls and readable status without per-cell DOM ownership. A pure transition boundary makes timing, randomization and difficult board fixtures reproducible. Avoid parallel sources of truth: score belongs to the session, not the view, and keyboard repeat belongs to the application, not browser-dependent key-repeat timing.

Use focused domain tests for geometry/transactions, application tests with explicit clocks and sequences, and headless browser checks for integrated input, rendering and lifecycle. [DECOMPOSITION](DECOMPOSITION.md) defines logical interfaces when available; [SPEC](SPEC.md) owns observable contracts when available. No runtime or performance claim follows from this design.
