# Tetris Web App — Requirements Analysis

## 1. Overview

**Project:** Tetris Web App  
**Tech Stack:** React + TypeScript  
**Target:** Single-player, browser-based, modern minimalist visual style  
**Goal:** Build a polished, deployable Tetris game with standard mechanics, responsive controls, and clean UI.

---

## 2. Functional Requirements

### 2.1 Core Game Mechanics

| ID | Requirement | Priority |
|---|---|---|
| FR-001 | **Game Board:** A 10×20 grid (standard Tetris playfield) rendered in the browser. | Must |
| FR-002 | **Tetrominoes:** Seven distinct pieces (I, O, T, S, Z, J, L) spawn at the top center. | Must |
| FR-003 | **Piece Rotation:** Clockwise and counter-clockwise rotation with wall-kick support. | Must |
| FR-004 | **Piece Movement:** Left, right, and soft drop (accelerated downward movement). | Must |
| FR-005 | **Hard Drop:** Instant drop to the lowest valid position. | Must |
| FR-006 | **Gravity:** Pieces fall at a rate determined by current level. | Must |
| FR-007 | **Line Clearing:** Complete horizontal lines are removed; lines above shift down. | Must |
| FR-008 | **Game Over:** Triggered when a new piece cannot spawn (collision at top). | Must |
| FR-009 | **Hold Piece:** Player can swap the current piece with a held piece (once per spawn). | Should |
| FR-010 | **Next Piece Preview:** Display the upcoming 1–3 pieces. | Should |
| FR-011 | **Ghost Piece:** Show a translucent preview of where the current piece will land. | Should |

### 2.2 Scoring & Leveling

| ID | Requirement | Priority |
|---|---|---|
| FR-012 | **Scoring System:** Points awarded per line clear (single, double, triple, Tetris). | Must |
| FR-013 | **Level Progression:** Level increases every 10 lines cleared; gravity speed increases. | Must |
| FR-014 | **High Score:** Persist highest score in localStorage. | Should |
| FR-015 | **Score Display:** Real-time score, level, and lines-cleared count visible during play. | Must |

### 2.3 Controls

| ID | Requirement | Priority |
|---|---|---|
| FR-016 | **Keyboard Controls:** Arrow keys / WASD for movement; Up/W for rotation; Space for hard drop; C for hold; P for pause. | Must |
| FR-017 | **Touch Controls (Mobile):** On-screen directional pad + action buttons for mobile play. | Should |
| FR-018 | **Pause/Resume:** Game can be paused and resumed without state loss. | Must |
| FR-019 | **Restart:** Option to restart immediately after game over or during pause. | Must |

### 2.4 UI/UX

| ID | Requirement | Priority |
|---|---|---|
| FR-020 | **Start Screen:** Title, "Play" button, and high score display. | Must |
| FR-021 | **Game Screen:** Board, score panel, next/hold previews, pause button. | Must |
| FR-022 | **Game Over Screen:** Final score, level reached, new high score indicator, retry button. | Must |
| FR-023 | **Visual Style:** Modern minimalist aesthetic — clean lines, subtle shadows, consistent color palette per piece. | Must |
| FR-024 | **Animations:** Smooth piece movement, line-clear flash effect, subtle spawn animation. | Should |

---

## 3. Non-Functional Requirements

| ID | Requirement | Target |
|---|---|---|
| NFR-001 | **Performance:** Game loop runs at 60 FPS; input latency < 16ms. | 60 FPS |
| NFR-002 | **Browser Compatibility:** Chrome, Firefox, Safari, Edge (last 2 versions). | Last 2 versions |
| NFR-003 | **Responsive Design:** Playable on desktop (keyboard) and mobile (touch) without layout breakage. | 320px–2560px width |
| NFR-004 | **Accessibility:** Keyboard-only playable; colorblind-friendly piece patterns (optional). | WCAG 2.1 AA |
| NFR-005 | **Bundle Size:** Production build < 200 KB gzipped (excluding assets). | < 200 KB |
| NFR-006 | **Offline Support:** Game functions without network after initial load (PWA-ready). | Service Worker |
| NFR-007 | **State Persistence:** Pause state survives page refresh (optional). | localStorage |

---

## 4. User Stories

### US-001 — Start the Game
> **As a** player, **I want** to press a "Play" button from the start screen, **so that** I can begin a new game.

- **Acceptance Criteria:**
  - Start screen displays on load.
  - Clicking "Play" transitions to the game screen.
  - A new piece spawns immediately.

### US-002 — Move and Rotate Pieces
> **As a** player, **I want** to move and rotate falling pieces, **so that** I can position them to complete lines.

- **Acceptance Criteria:**
  - Left/Right arrows move the piece one cell.
  - Up arrow rotates clockwise; Z rotates counter-clockwise.
  - Wall kicks allow rotation near edges and other pieces.
  - Invalid moves (collision, out of bounds) are rejected.

### US-003 — Clear Lines and Score
> **As a** player, **I want** completed lines to disappear and my score to increase, **so that** I feel rewarded for good play.

- **Acceptance Criteria:**
  - 1 line = 100 × level points
  - 2 lines = 300 × level points
  - 3 lines = 500 × level points
  - 4 lines (Tetris) = 800 × level points
  - Score updates immediately on clear.

### US-004 — Level Up
> **As a** player, **I want** the game to speed up as I clear more lines, **so that** difficulty increases over time.

- **Acceptance Criteria:**
  - Level increments every 10 lines cleared.
  - Gravity delay decreases by ~10% per level (capped at a minimum).
  - Level and lines-cleared are visible.

### US-005 — Game Over
> **As a** player, **I want** the game to end when pieces reach the top, **so that** there is a clear loss condition.

- **Acceptance Criteria:**
  - Game over triggers when a new piece collides on spawn.
  - Final score and level are displayed.
  - High score is updated if beaten.
  - "Play Again" button restarts the game.

### US-006 — Pause and Resume
> **As a** player, **I want** to pause the game, **so that** I can take a break without losing progress.

- **Acceptance Criteria:**
  - Pressing "P" or clicking the pause button freezes the game.
  - Resume button continues from the exact state.
  - Restart button starts a fresh game.

### US-007 — Play on Mobile
> **As a** mobile player, **I want** touch controls, **so that** I can play on my phone.

- **Acceptance Criteria:**
  - On-screen D-pad and action buttons are visible on touch devices.
  - Buttons are large enough for thumbs (min 44×44 pt).
  - Game board scales to fit the screen without horizontal scroll.

---

## 5. Tech Stack Recommendations

| Layer | Technology | Rationale |
|---|---|---|
| Framework | React 18+ | Component-based UI, strong ecosystem |
| Language | TypeScript | Type safety, better IDE support, fewer runtime bugs |
| Styling | CSS Modules or Tailwind CSS | Scoped styles, rapid development, responsive utilities |
| State | React Context + useReducer | Game state is centralized; no external library needed for scope |
| Game Loop | requestAnimationFrame | Smooth 60 FPS updates, browser-optimized |
| Build Tool | Vite | Fast dev server, optimized production builds |
| Testing | Vitest + React Testing Library | Unit tests for game logic, component tests for UI |
| Deployment | Static host (Vercel/Netlify) | Simple, free, CDN-backed |

---

## 6. Acceptance Criteria Summary (Task-Level)

- [x] All core Tetris mechanics documented (piece rotation, line clearing, gravity, game over)
- [x] User stories follow INVEST principles (Independent, Negotiable, Valuable, Estimable, Small, Testable)
- [x] Output is ready for design handoff

---

*Document version: 1.0*  
*Author: Bao (Business Analyst)*  
*Date: 2026-06-14*
