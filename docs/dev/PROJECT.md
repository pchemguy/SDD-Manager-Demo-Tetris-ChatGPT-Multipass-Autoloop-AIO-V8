# Browser Tetris

## Purpose and intended users

Build a small, playable, single-player Tetris game for desktop browser users with a keyboard. A player can open the page, play a complete game, see the score and restart after game over. The game runs entirely in the browser without an account or server service.

## Principal scope

- A 10-column, 20-row board with the seven standard tetromino shapes.
- A single falling piece, lateral movement, clockwise rotation, automatic gravity and keyboard soft drop.
- Collision handling against board boundaries and settled blocks; a rejected rotation leaves the piece unchanged.
- Locking on a failed downward movement attempt, completed-row removal and line-based scoring.
- A game-over state when the next piece cannot spawn, with an explicit restart that clears the board and score.
- A visible board, score, game status, restart action and concise keyboard instructions.

Use fixed gravity and independently sampled pieces to keep the game small and coherent. Exact timing, input bindings, spawn positions and scoring values belong to the behavioral specification.

## Desired qualities

Gameplay must remain responsive and deterministic for a supplied input sequence, piece sequence and elapsed game time. A piece may never lock outside the board or overlap settled blocks. Focus loss suspends gameplay and clears held inputs so returning to the tab cannot cause accumulated gravity or unintended movement.

Keep game rules independently verifiable, provide visible keyboard focus for HTML controls, and make game-over/restart status understandable without relying on piece colors alone. Verify browser behavior under the repository's [browser development policy](../../BROWSER_DEV_POLICY.md), with Chromium primary and Firefox secondary. No browser execution has been verified at the brief stage.

## Proposed technical direction

Use TypeScript for the client, Canvas for the board and ordinary HTML for controls and status. This keeps the rendered board compact while supporting direct keyboard interaction and independent rule tests. Static hosting is sufficient; Node is a development-tool runtime rather than a required deployed server.

DOM cell rendering is a reasonable alternative when individual cells need semantic interaction; that is outside this game's scope. A UI framework could manage interface state but adds machinery without an established benefit here. Architecture will settle structural boundaries and build tooling after brief acceptance.

## Scope exclusions

Hold, ghost pieces, bag randomization, wall kicks, hard drop, configurable locking, next-piece preview, penetrator bonuses and settings controls are outside the defined game. No cookies, URL configuration or saved game state are required. Multiplayer, accounts, backend leaderboards, touch controls and audio are excluded.

## Delivery and approval status

This is a proposed project brief, not an implemented product. The proposed initial playable release is 0.1.0, published only after its implementation is authorized, completed, verified and integrated. Versioning and release publication must reflect delivered functionality rather than document preparation.

Board dimensions, fixed gravity, baseline locking/random selection, technical direction, focus handling and exclusions beyond the supplied classic scope are agent proposals for human confirmation. No other material baseline question is currently identified; detailed contracts remain for the specification.
