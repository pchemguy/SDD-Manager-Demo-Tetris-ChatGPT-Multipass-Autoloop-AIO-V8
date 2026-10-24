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

An ordinary piece cannot move through occupied cells. A clockwise rotation that fails its initial placement is rejected. Choose each new kind independently with equal probability from the seven kinds, using an injected random sample in [0,1). Lock on any failed downward attempt, whether gravity or soft drop. These policies apply to the classic gameplay profile.

## B05 — Clock, suspension and event order

The application uses monotonic elapsed simulation time, never wall-clock calendar time. Hidden or unfocused documents suspend the game and clear held keys. Restore focus/visibility with a fresh clock anchor; do not advance by the hidden interval or resume held repeat without a new keydown. Process due scheduled events before a user command at the same simulation timestamp. At a shared deadline, gravity precedes key-repeat; stale events for a replaced piece are discarded. Process events in timestamp order so frame rate does not determine the result. Application integration owns this ordering.

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
