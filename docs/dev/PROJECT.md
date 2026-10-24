# Browser Tetris

## Purpose and users

Build a playable single-player game for desktop browser users with a keyboard. The player can open a static page, play a complete game, see score/status and restart. No account, backend service or deployed Node server is required.

## Principal scope

- A 10-column, 20-row board; seven tetrominoes; keyboard movement, clockwise rotation, fixed gravity, soft drop, line clearing and scoring; blocked-spawn game over and full restart.
- Hold, a landing ghost, 7-bag randomization, deterministic wall kicks and hard drop. Grounded pieces normally lock after a full gravity interval; a hard drop does not bypass that delay.
- Dynamic ghost visibility: show the projected piece only when every projected cell is in the lower half. A piece straddling the midline is hidden.

## Experience and quality

Use TypeScript, a Canvas board and ordinary HTML controls/status. Keep game rules independently testable from rendering, browser time and storage. A supplied piece sequence, ordered inputs and elapsed simulation time must produce repeatable outcomes. Loss of focus freezes game time and clears held keys; returning does not accumulate gravity. A legal lock is entirely within the board and does not overwrite settled cells.

Provide visible keyboard instructions, focus and game status; never communicate game over solely through colors. Chromium is primary and Playwright-managed Firefox secondary under the [browser policy](../../BROWSER_DEV_POLICY.md); headless interaction and screenshots are sufficient verification methods. Browser provisioning and actual gameplay remain unverified until implementation.

## Boundaries

- Multiplayer, accounts, service-backed leaderboards, touch input and audio.
- Penetrator mode and bonuses.
- Next preview and settings controls.
- Cookies, URL settings and saved game state.

## Delivery constraints

Start with a minimal playable release at 0.1.0 and increase minor versions for compatible capability increments, patch versions for fixes. Every authorized implementation phase requires complete verification, explicit integration, release notes, a matching version tag and a published GitHub release. [PLAN](PLAN.md) owns delivery boundaries when available; precise gameplay contracts belong to SPEC.
