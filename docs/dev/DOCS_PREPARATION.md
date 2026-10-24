# Main documentation preparation record

Current control and decision evidence; [DOCS_TASKS](DOCS_TASKS.md) owns checkboxes and [HANDOFF](HANDOFF.md) owns checkpoint continuity. Product documents describe only the current intended product.

## Current control

- Mode and source: autodoc/autoloop, explicitly requested for six cumulative scopes in the project seed.
- Multipass delivery mode: strict, the default; no flexible integration permission was supplied. Once established, earlier phase/task IDs, scope, milestone membership, ordering, dependencies and exits remain unchanged. Later scope is appended through bounded delivery increments.
- Current pass: 4, Penetrator mode; DOCS-002 accepted under scoped preapproval.
- Approval basis: first PROJECT and the proposed interaction rules approved by the user’s “Approve” response to proposal commit `f2e0d763ee168a52b5decff47e802552d23795cc`. Accordingly, ARCHITECTURE through TASKS and later PROJECT checkpoints are preapproved by the selected mode; later PROJECT approvals are waived, as announced before this checkpoint. New material later decisions are delegated to agent judgment with visible rationale and retained evidence.
- Tracking: enabled for documentation and implementation by existing root AGENTS policy. Documentation milestone 1 (`sdd-docs-main`) and issues #1–#9 were created and read back against the bundled standard definitions before any repository modification.
- Publication: every owned commit must be pushed/read back before further work. Main preparation stays on `design-docs/main`.
- Stop: after pass 6 DOCS-008 publication/issue closure; leave DOCS-009 and its issue and milestone open. No whole-package QC, documentation integration, implementation activation or product release is selected by this request.
- Reporting: Standard after initial explicit bootstrap; Minimal and Explicit remain available.

## Scope sequence

1. **Playable classic baseline:** Falling tetrominoes, movement, rotation, gravity, line clearing, scoring, game over and restart. Minimal coherent game only; no later enhancements or configuration.
2. **Gameplay enhancements:** Hold, ghost, 7-bag randomization, wall kicks, hard drop and a default full-gravity-interval grounded lock delay, including hard drop.
3. **Conditional ghost visibility:** Hide projected landing positions above the midline and show them in the lower half.
4. **Penetrator mode:** Bonus-funded hotkey activation for the current falling piece until lock; occupied cells survive traversal; locks require entirely in-board non-overlap. Penetrator hard drop and ghost use the lowest valid landing through blockers. Four-line clears award one bonus up to three. Activated pieces are white, regular pieces are not; one side-panel symbol per available bonus, updated on earning/spending.
5. **Session-only game configuration:** Side-panel ghost mode (hidden/dynamic/shown), hard drop enable, next preview enable, hard-drop lock policy (general/immediate), general locking policy (failed down/full grounded gravity interval), and Hold enable. Add next preview. Settings survive restart within the page but reset on reload; no persistence yet.
6. **Configuration persistence:** Resolve each setting independently by valid explicit URL value, saved cookie, then default. Setting changes save the cookie and update its URL parameter. Valid explicit URL values also save cookies even when equal to defaults. Omitted parameters retain cookies. Preserve all six controls and sensible defaults.

## Per-pass decisions

All entries below originate during pass 1 exploration. User-specified capabilities are requirements; additional resolutions were agent proposals accepted by the user’s “Approve” response on 2026-10-24. This confirms the stated cross-scope rules without adopting future capabilities into the baseline brief. “Proposed” in the retained source/basis cells identifies authorship; each applicable resolution is accepted.

| Pass / decision | Resolution and rationale | Basis / source | Applicability / status |
| --- | --- | --- | --- |
| 1 / Scope isolation | A complete minimal classic game; future scope remains in this record until adopted. | Explicit cumulative seed and strict default. | All passes; required. |
| 1 / Platform | TypeScript with a Canvas board and ordinary HTML controls; a static client with no backend. Prefer this over a UI framework for a small keyboard game; retain testable game rules independent of display/time. | Agent proposal; compared with DOM cell rendering and framework-managed rendering. DOM is an alternative for semantic per-cell controls; a framework adds state/tooling overhead without a requested need. | All passes; proposed. |
| 1 / Baseline rules | A 10 by 20 visible board, seven tetromino types, clockwise rotation rejected on collision without kicks, independent uniform piece selection, fixed gravity, soft drop, line-based scoring, blocked-spawn game over, complete restart. Baseline locks on a failed downward attempt. | Agent proposal to keep baseline coherent and bounded. Exact controls, score table and gravity value belong to SPEC. | Pass 1 onward; proposed. Pass 2 explicitly replaces randomization, rotation correction and default locking behavior through new scope. |
| 1 / Product boundary | Desktop keyboard play; no multiplayer, account system, leaderboard service, touch controls, audio or background gameplay. Loss of focus freezes time and clears held inputs; resume does not accumulate hidden-tab gravity. | Agent proposal to avoid unintended scope and timing surprises. | All passes; proposed. |
| 1 / Ghost midline | Classify by the highest occupied cell of the projected piece, not its bounding-box center. Show only when every projected cell is in the lower half; on a 20-row board this means minimum row at least 10. A straddling piece is hidden; the boundary row is lower-half. | Agent proposal to make straddling behavior unambiguous and conservative. | Passes 3–6; proposed. Pass 2 ghost is always visible. |
| 1 / Lock timer | Start a full current gravity interval on first contact. Horizontal motion and rotation while grounded do not reset it. Becoming airborne cancels it; re-grounding begins a new full interval. Freeze it with suspended game time. Use elapsed simulation time, not the remaining gravity tick. | Agent proposal to satisfy the full-interval requirement without unlimited grounded resets. | Passes 2–6; proposed. |
| 1 / Hard-drop timer | A drop that newly establishes contact gets the full interval; a drop on an already grounded piece does not restart its timer. Under failed-down locking, hard drop positions the piece and the next failed downward attempt locks it; the immediate override locks in the same command. | Agent proposal; reconciles the two selectable policies without a zero-distance reset loophole. | Passes 2–6, immediate override from pass 5; proposed. |
| 1 / Hold lifecycle | One successful Hold per active piece; empty Hold consumes the next piece, a swap does not; incoming pieces start at spawn orientation with fresh timing. Disable Hold while a penetrator is active, including hotkeys. Rejected Hold neither spends bonuses nor changes the piece. | Agent proposal consistent with a penetrator lasting until lock. | Passes 2–6; active penetrator restriction from pass 4; proposed. |
| 1 / Penetrator activation | One bonus spent atomically on successful activation; repeated activation has no effect. Regular collision-free active pieces may activate, including while grounded; activation recomputes the terminal landing and airborne/contact state. Existing grounded time is retained if contact remains. | Agent proposal preventing repeated spending and timer reset exploits. | Passes 4–6; proposed. |
| 1 / Penetrator descent | Intermediate overlap is allowed without changing settled cells. For each position/orientation, scan all downward in-board placements and choose the lowest collision-free placement at or below the current row, ignoring intervening blockers. That is the terminal ground position for gravity, soft/hard drop and ghost. Horizontal/rotation candidates require a legal terminal placement at or below their candidate row; otherwise reject them. Never lock at an overlapping position. | Agent proposal ensuring slow descent, hard drop and ghost share a legal landing, including sealed cavities. | Passes 4–6; proposed. |
| 1 / Penetrator completion | Only a successful legal lock ends penetrator status and allows normal line clearing. Four simultaneous cleared rows award one bonus after lock, capped at three; new games begin with zero. Board/held/next regular pieces use non-white colors; active penetrator and its visible ghost convey white status, with ghost styling kept distinct. | Bonus and color requirements from seed; lifecycle/start count and ghost styling are proposed. | Passes 4–6; mixed requirement/proposal. |
| 1 / Settings application | Visibility, preview, hard-drop enable and Hold enable update immediately. Lock-policy changes update the selected setting immediately but take effect for the next spawned/swapped piece; display that pending effect. Changes do not reset, move or unlock the current piece. Disabling Hold preserves its stored piece. | Agent proposal to prevent retroactive locks and timing resets. | Passes 5–6; proposed. |
| 1 / Settings defaults | Dynamic ghost, hard drop on, next preview on, hard drop follows general locking, full grounded gravity interval, Hold on. Restart preserves settings and resets game/held piece/bonuses; page reload uses defaults in session-only mode. | Agent proposal matching the evolved gameplay defaults. | Passes 5–6; proposed. |
| 1 / Input validation | Validate each source independently. Invalid URL values fall back to a valid cookie then default; invalid cookies fall back to default. Use a documented finite exact value vocabulary and first URL occurrence if duplicated. Do not save invalid URL input over a valid cookie. | Agent proposal; seed specifies precedence but not malformed/duplicate handling. | Pass 6; proposed. |
| 1 / Persistence effects | Save valid explicit URL values to cookies, including defaults, without overwriting cookies for omitted settings. UI changes use History replacement, preserving other query parameters and fragment without reload. Cookie/history failures retain playable in-memory settings and expose a non-blocking persistence status. Cookies contain settings only. | Core precedence/write rules from seed; failure and URL-handling behavior proposed. | Pass 6; mixed requirement/proposal. |
| 1 / Versions and releases | First verified integrated playable baseline targets 0.1.0. Subsequent compatible capability increments increase the minor version; corrective releases increase patch. Final phase count and versions belong to PLAN. Each subsequently authorized completed implementation phase requires verified integration, release notes, tag and published GitHub release. No release for document preparation. | Version policy proposed under explicit version-management delegation; release boundary required by seed. | Implementation only; recorded for later planning. |
| 1 / Browser evidence | Chromium primary and Playwright-managed Firefox secondary under BROWSER_DEV_POLICY. Headless interaction/screenshots suffice. Provisioning remains unverified until implementation setup; follow proactive diagnostics and isolated fallbacks, reporting any concrete unresolved browser blocker. | Existing repository policy; headless approach proposed. | Implementation verification; required policy/proposed method. |

## Cross-scope decisions

| Concern | Decision / applicable scopes | Reconsideration condition |
| --- | --- | --- |
| Ghost and penetrator landing | Ghost-midline and penetrator-descent rows above govern passes 3–6. Visibility never changes landing calculation; a hidden ghost still has a computed target. | Board geometry or landing semantics change. |
| Contact and configuration | Lock-timer, hard-drop-timer, activation and settings-application rows govern passes 2–6. Same-timestamp inputs and timeout ordering must be made deterministic in SPEC. | New speed rules, pause behavior or a requested timer-reset policy. |
| Penetrator and Hold | Hold-lifecycle and penetrator-completion rows prevent storing or swapping an activated penetrator. | Human changes the until-lock lifecycle. |
| Persistence versus live game | Settings-application, defaults and persistence rows separate chosen configuration from current-piece timing policy. Reload restores configuration but never a running game. | Game-state persistence is requested. |
| Minimal increment and later delivery | Scope-isolation and version rows preserve prior pass ranges while later phases modify shared code. No future-scope acceptance gates are added to earlier phases. | Explicit flexible-multipass permission or a scoped human amendment. |

### Scope 2 entry

Scope 1 completed at `7f874981df6d59b5523c510f44fcbc1a39b52ab2` with document publication and issue closures verified. Carry forward the approved cross-scope decisions; no unresolved material conflict. Protect all existing PLAN/TASKS phase blocks; append scope 2 delivery work only. Later document acceptance uses the recorded autoloop preapproval.

### Scope 2 decisions

Delegated contract precision: explicit clockwise SRS offset tables, with a separate I table and positive-down coordinates, verified against author-published data; Up rotation, C/Shift Hold and Space hard drop are edge-triggered. No counterclockwise/180 command is added. Fixed 1000 ms gravity and approved contact/reset rules remain. The modern-handling phase groups shared piece-lifecycle changes into three bounded milestones; prior baseline remains protected. Basis: delegated agent judgment under the user-approved autodoc/autoloop sequence; applicable to this and subsequent scopes. Status: active; reconsider if the related gameplay or persistence contract changes.

### Scope 3 entry

Scope 2 completed at `93d3ad4fe5fe2c96282c692d313c00f8a17001dd` with document publication and issue closures verified. Carry forward the approved cross-scope decisions; no unresolved material conflict. Protect all existing PLAN/TASKS phase blocks; append scope 3 delivery work only. Later document acceptance uses the recorded autoloop preapproval.

### Scope 3 decisions

Carry forward the human-approved highest-occupied-row classification (minimum y at least 10). No new behavior choice: visibility is a pure predicate over the existing landing. A single three-task delivery milestone is retained because another split would add overhead to a narrow rendering capability. Basis: delegated agent judgment under the user-approved autodoc/autoloop sequence; applicable to this and subsequent scopes. Status: active; reconsider if the related gameplay or persistence contract changes.

### Scope 4 entry

Scope 3 completed at `6955447c6583c2aff467828fb9335bf692ca348f` with document publication and issue closures verified. Carry forward the approved cross-scope decisions; no unresolved material conflict. Protect all existing PLAN/TASKS phase blocks; append scope 4 delivery work only. Later document acceptance uses the recorded autoloop preapproval.

### Scope 4 decisions

Carry forward terminal-search, active Hold exclusion, bonus cap and timing rules. Delegated visual precision: settled cells use their non-white kind color after ability ends; the visible active penetrator/ghost indicates white mode without retaining ability in settled cells. Candidate rotations use the same ordered kick offsets with penetrator-specific terminal legality. Two milestones separate traversal/lifecycle from reward/UI acceptance. Basis: delegated agent judgment under the user-approved autodoc/autoloop sequence; applicable to this and subsequent scopes. Status: active; reconsider if the related gameplay or persistence contract changes.

## Decisions and document evidence

| Task | Current evidence / decision basis |
| --- | --- |
| DOCS-001 | Initialization commit `a8a958614771408144432618bc4e9f82ef8cecfc` published and exact remote ref verified. Four pre-existing root files preserved against initial commit `3cec5836208ffe62881ab5f4aec809152c962bdb`; records and checked DOCS-001 committed together. Issue #1 closed as completed and read back. |
| DOCS-002 | Pass 4: PROJECT.md SHA-256 `0223212f979446e67e70b1421a4c04d2a162d4b72d3f0e8a08992768dda2257a`. Accepted by autodoc/autoloop scoped preapproval after the first human PROJECT acceptance. Owner QC: current-scope conformance, ownership, links and content boundary checked; required adjacent report included where applicable. Publication/issue closure follows this commit. |
| DOCS-003 | Pass 3: ARCHITECTURE.md SHA-256 `57f71a70e3d48982fdd2804e44feef8e3e5d4113f31148e989ca75d8288af324`. Accepted by autodoc/autoloop scoped preapproval after the first human PROJECT acceptance. Owner QC: current-scope conformance, ownership, links and content boundary checked; required adjacent report included where applicable. Publication/issue closure follows this commit. |
| DOCS-004 | Pass 3: DECOMPOSITION.md SHA-256 `8bab4a2726e8c99bd243361b9653c0c9022597a23772ea1530bac74a1b72b6d0`. Accepted by autodoc/autoloop scoped preapproval after the first human PROJECT acceptance. Owner QC: current-scope conformance, ownership, links and content boundary checked; required adjacent report included where applicable. Publication/issue closure follows this commit. |
| DOCS-005 | Pass 3: SPEC.md SHA-256 `959dd151792880656c0bb6cc19c0ec1567000679b2fa715d54590ff9fdceccbb`; SPEC-REVIEW-REPORT.md SHA-256 `fc1180b8008ccab31e66866651b3bd806c24e5b6aed56b4cdb5f1795b188c717`. Accepted by autodoc/autoloop scoped preapproval after the first human PROJECT acceptance. Owner QC: current-scope conformance, ownership, links and content boundary checked; required adjacent report included where applicable. Publication/issue closure follows this commit. |
| DOCS-006 | Pass 3: PLAN.md SHA-256 `b3105c44acf273f2abb154676d3ce425f210d36a18bb1f7435b8481f7554a504`; PLAN-REVIEW-REPORT.md SHA-256 `3ec8346049c1a6e83f1e5a8f509a8e8b1a28520dbd34ecdb52b5d392dfc1ec1f`. Accepted by autodoc/autoloop scoped preapproval after the first human PROJECT acceptance. Owner QC: current-scope conformance, ownership, links and content boundary checked; required adjacent report included where applicable. Publication/issue closure follows this commit. |
| DOCS-007 | Pass 3: layout.md SHA-256 `42e5d2a5f87a60d740746791bd995cbe51c329228df5d81d505c2bd28a767177`; PLAN-REVIEW-REPORT.md SHA-256 `60d7a37617cf98ae6e0f2db19f729069d4599df6a9974863f1b30e38dc34d99b`. Accepted by autodoc/autoloop scoped preapproval after the first human PROJECT acceptance. Owner QC: current-scope conformance, ownership, links and content boundary checked; required adjacent report included where applicable. Publication/issue closure follows this commit. |
| DOCS-008 | Pass 3: TASKS.md SHA-256 `2ceb58c0fb5502e6da33757e20e3320504c9a53e4133d86f2fff75096bfb4eb9`; TASKS-REVIEW-REPORT.md SHA-256 `ed4176fb336ad93e6c9f9fcb0f35738762cb2af308ca35566ee8ad40f4e632b3`. Accepted by autodoc/autoloop scoped preapproval after the first human PROJECT acceptance. Owner QC: current-scope conformance, ownership, links and content boundary checked; required adjacent report included where applicable. Publication/issue closure follows this commit. |
| DOCS-009 | Not selected; remains pending after final autoloop pass. |

Material unresolved decisions: none blocking current document authoring. Agent-resolved contract precision remains delegated. No implementation is authorized.

## Initialization and current reset

- Original presence: all four existed. Retained `AI_DISCLOSURE.md`, `SDD-MANAGER.md`, `AGENTS.md`, `SKILL_DISCOVERY_PROTOCOL.md`; copied none.
- Verification: compare each retained file byte for byte with the initial committed blob; preserve both policy files and packaged plugin content unchanged. Task template from the repository-bundled SDD Manager 0.15.2, pinned by initial commit; only DOCS-001 checkbox changes.
- Continuation: all-present case; no mixed-initialization hold.
- Manual provenance: default enabled. Base `3cec5836208ffe62881ab5f4aec809152c962bdb`; seed `78e7be01a43b8a26033ce67c2565845bd64cec19` on `design-docs/ai-logs`; explicit two-parent merge `5bc22f5535bff34275d6d7c672ed81e25471ed4b` on `main`. Both remote refs exactly read back; packaged scaffold bytes verified before each commit. No transcript generated.
- Preparation branch: `design-docs/main`, created from published `main` at `5bc22f5535bff34275d6d7c672ed81e25471ed4b`.
- Credential continuity: ignored, untracked root `gh.tkn`; value excluded from evidence and commits. Required ignore rule integrated with scaffold.
- Current reset: scope 3 completed through DOCS-008 at `6955447c6583c2aff467828fb9335bf692ca348f`; authorized predefined autoloop reset to scope 4.

## Pending transitions

Publish/read back the owning completion commit and close/read back issue #2. Then continue with DOCS-003. Reconcile real state before replay.
