# Behavioral specification

## Context and owners

The game is a static single-player desktop browser application defined by [PROJECT](PROJECT.md). [ARCHITECTURE](ARCHITECTURE.md) owns dependency direction and [DECOMPOSITION](DECOMPOSITION.md) owns the named components. Contracts below are canonical behavior; test fixtures may inject random values and elapsed simulation time without becoming public game controls.

## B01 — Board and piece geometry

Use columns x=0..9 and rows y=0..19, increasing right/down. Empty cells and occupied colored cells are distinct values. All active/settled pieces consist of four occupied cells. Spawn masks, as slash-separated rows, are I `0000/1111/0000/0000`, J `100/111/000`, L `001/111/000`, S `011/110/000`, T `010/111/000`, Z `110/011/000`, O `11/11`. A 1 denotes an occupied cell. Rotate square masks clockwise by `(x,y) → (n−1−y,x)`; O remains unchanged. Spawn at mask origin `(floor((10−n)/2),0)` in orientation zero. Only occupied cells, not empty mask padding, must fit bounds. Geometry owns cell transformations; Board owns occupancy validation.

## B02 — Session, input and gravity

Start playing with an empty board, score zero and one spawned piece. Left/Right move one column, Up rotates clockwise, Down soft-drops one row, and the HTML Restart action starts a fresh game. A non-repeat keydown acts once; browser autorepeat events are ignored. Held lateral/Down keys repeat after 150 ms, then every 50 ms; the most recently pressed lateral direction wins. Rotation is edge-triggered. Gameplay keys prevent page scrolling only while the game surface owns focus; controls retain normal keyboard behavior.

Gravity attempts one downward row every 1000 ms of active simulation time, first due 1000 ms after each spawn; there are no levels or automatic speed increases. Commands do not postpone gravity. Invalid movement/rotation leaves state unchanged. Restart clears the board, score, active/held-input state and stream state. A spawn overlapping settled cells ends the game; gameplay commands then have no effect. Restart is always available. GameSession owns status and spawn; GameController owns ordered input/time.

## B03 — Legal lock, clearing and score

A lock writes exactly four in-board, non-overlapping cells atomically. Remove every full row simultaneously, shift remaining rows down while preserving order, and insert empty rows at the top. Award 100/300/500/800 points for 1/2/3/4 rows, respectively; no drop or time points. Then spawn the next piece. A failed spawn preserves the completed lock/clear/score and changes status to game over. Board and GameSession participate in this transaction; rendering cannot observe a partial result.

## B04 — Basic movement policies

An ordinary piece cannot move through occupied cells. Enhanced gameplay uses H01 randomization, H02 rotation correction and H04 locking. Ordinary collision boundaries remain in force; mode-specific traversal may be defined separately. The 0.1.0 classic delivery profile uses independent uniform kind selection, rejects an initially blocked rotation and locks on failed down; that bounded delivery acceptance is preserved in PLAN.

## B05 — Clock, suspension and event order

The application uses monotonic elapsed simulation time, never wall-clock calendar time. Hidden or unfocused documents suspend the game and clear held keys. Restore focus/visibility with a fresh clock anchor; do not advance by the hidden interval or resume held repeat without a new keydown. Process due scheduled events before a user command at the same simulation timestamp. At a shared deadline, lock expiry precedes gravity, then key-repeat; stale events for a replaced piece are discarded. Process events in timestamp order so frame rate does not determine the result. Application integration owns this ordering.

## B06 — View, controls and failures

Draw the board and current piece with distinct non-white colors, cell boundaries and readable score/status. Show keyboard instructions, game-over status and Restart. HTML controls have labels and visible focus. At a 1280×800 desktop viewport, board and core controls must be usable without clipping; resizing cannot mutate game state. Focus suspension is visible. No multiplayer, accounts, audio or touch interface is required. No runtime game-state persistence is required. Browser provisioning and required Chromium/Firefox checks follow the root policy; failures are reported rather than silently skipped.

## Core acceptance

| ID | Observable condition / evidence to obtain |
| --- | --- |
| A01 | Each shape spawns and rotates; wall/floor/occupied collisions reject illegal ordinary moves without changing settled cells. |
| A02 | Explicit clock and input fixtures reproduce gravity, repeat, suspension and shared-deadline ordering. |
| A03 | Single, adjacent and separated multiple-row clears compact correctly and award the exact table score. |
| A04 | Blocked spawn produces visible game over; Restart removes all prior board/score/input state. |
| A05 | Chromium and Firefox headless interaction validates keyboard movement, rotation, soft drop, status, focus suspension and restart; inspect representative screenshots for clipping/readability. |

## H01 — Seven-bag and Hold

PieceStream shuffles exactly I,J,L,O,S,T,Z using Fisher–Yates: for i=6 down to 1 choose j=floor(r×(i+1)) for r in [0,1), then swap. Consume all seven before refilling. H01 supplies randomization for enhanced gameplay. A C or Shift edge-triggered command holds once until the active piece locks. Empty Hold stores the active kind and consumes the next stream kind; nonempty Hold swaps without advancing the stream. Incoming pieces use spawn orientation/position and fresh timing; a failed spawn causes game over. Only a successful Hold sets hold-used. Show the held kind; rejected/repeated commands consume nothing. Restart empties Hold and resets its usage flag.

## H02 — Wall kicks and landing

Orientations are 0, R, 2, L in clockwise order. For a clockwise rotation, try the following ordered mask-origin offsets relative to basic rotation, in B01 coordinates (positive y downward); accept the first legal candidate or reject unchanged. O rotation is a no-op. No counterclockwise or 180-degree command is required.

| Transition | J, L, S, T, Z offsets | I offsets |
| --- | --- | --- |
| 0 → R | (0,0), (-1,0), (-1,-1), (0,2), (-1,2) | (0,0), (-2,0), (1,0), (-2,1), (1,-2) |
| R → 2 | (0,0), (1,0), (1,1), (0,-2), (1,-2) | (0,0), (-1,0), (2,0), (-1,-2), (2,1) |
| 2 → L | (0,0), (1,0), (1,-1), (0,2), (1,2) | (0,0), (2,0), (-1,0), (2,-1), (-1,2) |
| L → 0 | (0,0), (-1,0), (-1,1), (0,-2), (-1,-2) | (0,0), (1,0), (-2,0), (1,2), (-2,-1) |

Offset reference: [author-published SRS data](https://gist.github.com/Shuflduf/e5186328dce8ab7d38a16d73971abcee). The explicit table is the contract; there is no external runtime dependency.

 Normal landing is the greatest downward displacement reachable by consecutive legal down moves before the first blocked move. LandingSolver returns exact occupied cells; ghost and hard drop consume the same result. Ghost draws behind the active piece with a distinct translucent/outline style and cannot obscure settled cells. Ghost visibility is governed by G01; it is not a second active piece.

## H03 — Hard drop

Space is edge-triggered hard drop. Move the piece directly to its computed landing without intermediate board writes. Repeated browser key events are ignored. A newly grounded piece starts its normal grounded timer; a zero-distance hard drop on an already grounded piece retains elapsed contact time. Hard drop does not itself imply immediate lock. Drop awards no score.

## H04 — Grounded interval locking

Enhanced gameplay uses a full 1000 ms contact interval instead of the basic failed-down lock. Start the contact deadline when a spawn, move, rotation or drop first has no permitted downward progress. Grounded lateral movement, rotation, failed down and zero-distance hard drop do not reset it. Becoming airborne cancels the deadline; a later contact starts a fresh full interval. Lock at the exact deadline only if the current piece is legally grounded. Suspension freezes elapsed contact time. Hold creates a new piece with new timing and invalidates the old deadline. Basic geometry/scoring/suspension remain applicable; enhanced kick/random/lock policies govern where specified.

## Enhanced acceptance

| ID | Observable condition / evidence to obtain |
| --- | --- |
| A06 | Every aligned seven-piece bag is a permutation; boundary refill and Hold stream consumption are exact. |
| A07 | Kicks choose the first legal offset or leave rotation unchanged; ghost cells equal hard-drop cells for all shapes and obstruction fixtures. |
| A08 | Contact at t locks at t+1000, not the next partial gravity tick; grounded moves/failed down/drop do not reset; airborne and Hold cancel old deadlines. |
| A09 | Browser checks exercise Hold once-per-piece, hard drop and ghost, plus classic scoring/game-over/restart and focus regressions. |

## G01 — Dynamic ghost visibility

Compute landing even when hidden. Under dynamic visibility, draw the ghost only if `min(projected occupied y) >= 10`. Thus a straddling piece and any piece with a cell above row 10 are hidden; a piece whose highest cell is row 10 is shown. Re-evaluate after every position/orientation/board change. Visibility has no effect on drop, input, collision or lock time. GhostVisibility owns classification; GameView consumes it.

Acceptance A10: fixtures with highest projected rows 9, 10 and 11, including tall/straddling shapes and transitions in both directions, verify visibility and unchanged landing/timing. Repeat a representative browser interaction and screenshot.
