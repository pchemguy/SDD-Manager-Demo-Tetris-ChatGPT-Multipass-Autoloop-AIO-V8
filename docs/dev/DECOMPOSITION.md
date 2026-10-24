# Component decomposition

## Responsibility model

Components refine the blocks in [ARCHITECTURE](ARCHITECTURE.md). Their interfaces below describe ownership and collaboration; SPEC supplies exact behavior when available. Components are ordinary modules with explicit inputs rather than mandatory classes.

| Component | Provides and owns | Requires / consumers | Verification seam |
| --- | --- | --- | --- |
| Geometry | Immutable shape masks, orientations, occupied-cell coordinates and translations. | Shape/orientation values only; GameSession validates resulting cells through Board. | Fixtures for each orientation and edge. |
| Board | Settled cell grid, placement checks and atomic placement/row compaction. | Cell-coordinate values; returns cleared-row count and a new grid. | Consecutive/nonconsecutive/full-board clears and rejected overlap. |
| PieceStream | Owns a Fisher–Yates shuffled seven-piece bag and cursor; can peek without consumption. | Injected uniform random-source port. | Every bag is a permutation; empty Hold consumes exactly once. |
| GameSession | Owns board/active/held state, hold-used flag, contact deadline, score and status; coordinates kicks, drops, hold and legal-lock transactions. | Geometry, Board, PieceStream and LandingSolver. | Hold/top-out, grounded motion and hard-drop timing traces. |
| GameController | Orders commands and due simulation events; owns held-key repeat and suspension anchors. | Session transitions and monotonic clock samples; no board writes. | Exact deadlines, focus gaps and keyup/repeat ordering. |
| GameView | Draws Canvas from snapshots; owns DOM status/instructions/restart event binding. | Read-only snapshots and controller commands; no collision rules. | Browser input/status and screenshot inspection. |
| LandingSolver | Computes projected landing cells without mutating the board or consuming time. | Geometry plus occupancy; GameSession and GameView consume the same result. | Drop/ghost agreement and obstruction boundaries. |
| GhostVisibility | Classifies projected occupied cells relative to the midline; never changes the target. | LandingSolver result and selected display mode when configurable. | Upper/lower/straddling fixtures. |

## Collaboration and lifecycle

The browser shell forwards input and monotonic time to GameController. Controller serializes transitions through GameSession and delivers a coherent snapshot to views. GameSession alone decides whether a candidate moves or locks. Board applies settled-cell writes only after complete validation, compacts full rows and returns the count for session-owned scoring. Game over accepts restart and ignores gameplay commands.

Restart creates fresh board/session/stream state and clears input repeat state. Visibility/focus loss pauses simulation rather than destroying the session. Rendering can be repeated without side effects. Avoid circular dependencies: views consume controller/snapshot contracts, controller consumes the domain, and domain helpers consume domain values only. Shared types describe values; they do not become a second state store.

## Boundary review

Each rule has one authoritative owner and each clock/random/browser dependency can be supplied explicitly. A transition may coordinate several closely related domain modules without introducing a service layer. Recoverable browser failures are contained at the browser-facing boundary. No component is required solely for speculative reuse; physical allocation belongs to layout.
