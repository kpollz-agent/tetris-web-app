# Tetris Web App — UX/UI Design Deliverables

## Summary

Complete UX/UI design package for a modern minimalist Tetris web app. Design supports all BA requirements (core mechanics, scoring, controls, responsive play) and is ready for development handoff.

---

## 1. Design Philosophy

**Modern Minimalist** — Clean, distraction-free interface that puts the game first. Every visual element serves a purpose. No ornamental chrome, no gradients, no noise.

**Core Principles:**
- **Clarity over decoration** — UI elements are geometric, flat, and precise
- **Color as information** — Each tetromino has a distinct, consistent color
- **Responsive by default** — Single layout that adapts from mobile (320px) to ultrawide (2560px)
- **Accessibility baked in** — WCAG 2.1 AA compliant contrast, keyboard-only playable, colorblind-friendly patterns

---

## 2. Color Palette

### Tetromino Colors
| Piece | Hex |
|-------|-----|
| I (cyan) | `#00F0F0` |
| O (yellow) | `#F0F000` |
| T (purple) | `#A000F0` |
| S (green) | `#00F000` |
| Z (red) | `#F00000` |
| J (blue) | `#0000F0` |
| L (orange) | `#F0A000` |

### UI Colors
| Role | Hex |
|------|-----|
| Background | `#0D0D0D` |
| Surface | `#1A1A1A` |
| Elevated | `#262626` |
| Border | `#404040` |
| Text Primary | `#FFFFFF` |
| Text Secondary | `#A3A3A3` |
| Accent (CTA) | `#00F0F0` |
| Success | `#00F000` |
| Danger | `#F00000` |

### Colorblind Patterns
Each piece has a subtle geometric pattern overlay (CSS `background-blend-mode`): I=stripes, O=solid, T=crosshatch, S=dots, Z=v-stripes, J=chevron, L=grid. Toggle in settings.

---

## 3. Typography

| Role | Font | Weight | Size |
|------|------|--------|------|
| Game Title | Inter | 800 | 48px |
| Screen Title | Inter | 700 | 32px |
| Score/Numbers | JetBrains Mono | 700 | 28px |
| Labels | Inter | 500 | 14px |
| Body | Inter | 400 | 16px |
| Button | Inter | 600 | 16px |
| Small/Hints | Inter | 400 | 12px |

**Font Stack:** `Inter` (primary), `JetBrains Mono` (scores/numbers).

---

## 4. Layout System

- **Base unit:** 4px
- **Spacing scale:** 4, 8, 12, 16, 24, 32, 48, 64, 96
- **Board cell sizes:** 24px (desktop) / 20px (tablet) / 16px (mobile) / 14px (mobile S) / 28px (desktop L) / 32px (ultrawide)
- **Border radius:** 4px (UI), 0px (board — sharp precision)
- **Container max-width:** 960px (centered)

---

## 5. Screen Designs

### 5.1 Start Screen
- Centered layout (max-width 400px)
- Logo: JetBrains Mono 48px, cyan accent on "I"
- High score display (JetBrains Mono 28px)
- Primary CTA: "PLAY" — cyan bg, dark text, 56px height
- Secondary: "HOW TO PLAY" — bordered, transparent bg
- Controls hint at bottom

### 5.2 Game Screen — Desktop (1024px+)
- **3-column layout:** Left panel (160px) | Board (240px) | Right panel (160px)
- **Header:** Logo left, pause icon button right (40px circle)
- **Left panel:** Hold preview (4×4 grid), Score, Lines
- **Center:** Game board — 10×20 grid, 24px cells, 240×480px total
- **Right panel:** Next preview, Level, Goal (lines to next level)
- **Panels:** Background #1A1A1A, border-radius 4px, padding 16px

**Game Board Details:**
- Border: 1px solid #404040
- Optional grid lines: 1px #262626 (toggleable)
- Active piece: Solid color + 3D inner highlight (top-left rgba(255,255,255,0.3), bottom-right rgba(0,0,0,0.3))
- Ghost piece: Same color, 30% opacity, no highlight
- Locked pieces: 90% brightness, no highlight

### 5.3 Game Screen — Mobile (320px–767px)
- **Vertical stack:** Header → Board → Stats row → Touch controls
- Board: 160×320px (16px cells)
- Stats row: Hold (48px preview) | Next (48px preview) | Score (mono 18px)
- Touch controls: Fixed 80px bottom bar
  - D-pad: ← ↓ → (56px square buttons, border-radius 8px)
  - Actions: ↻ (rotate), ⤓ (hard drop), H (hold) — 56px circular buttons
  - Background: #262626, active: #404040

### 5.4 Pause Overlay
- Background: rgba(0,0,0,0.85)
- Modal: 360px wide, #1A1A1A, border-radius 8px, padding 32px
- Title: "PAUSED" — 32px bold white
- Buttons: Resume (primary cyan), Restart (secondary bordered), Settings (tertiary text)

### 5.5 Game Over Screen
- Background: rgba(0,0,0,0.9)
- Title: "GAME OVER" — 32px bold red (#F00000)
- Final score: 48px mono in bordered box
- Stats: Level reached, Lines cleared — 16px secondary
- New high score: Green (#00F000) with pulse animation
- Actions: Play Again (primary), Main Menu (secondary)

### 5.6 How to Play Modal
- Header: "HOW TO PLAY" + close (×) button
- Controls section: Keyboard mappings with key badges
- Scoring section: 1/2/3/4 line clear multipliers
- CTA: "GOT IT" primary button

---

## 6. Component Specs

### Game Board
```
Width:  240px (desktop) / 200px (tablet) / 160px (mobile)
Height: 480px (desktop) / 400px (tablet) / 320px (mobile)
Cell:   24px / 20px / 16px
Border: 1px solid #404040
Background: #0D0D0D
```

### Piece Preview (Hold/Next)
```
Size: 4×4 grid (same cell size as board)
Background: #0D0D0D, Border: 1px solid #404040
Border-radius: 4px, Padding: 8px
Label: 12px uppercase #A3A3A3
```

### Score Panel
```
Background: #1A1A1A, Border-radius: 4px, Padding: 16px
Label: 12px uppercase #A3A3A3, letter-spacing 0.05em
Value: 28px JetBrains Mono #FFFFFF weight 700
```

### Buttons
**Primary:** Height 56px, bg #00F0F0, color #0D0D0D, Inter 600 16px, radius 4px. Hover: #33F3F3. Active: #00C0C0.
**Secondary:** Height 48px, transparent, border 1px #404040, color #FFFFFF. Hover: border #A3A3A3 + bg rgba(255,255,255,0.05).
**Icon:** 40px circle, transparent, border 1px #404040. Hover: bg rgba(255,255,255,0.1).

### Touch Controls
```
Height: 80px, bg #1A1A1A, border-top 1px #404040
Buttons: 56px × 56px, bg #262626, active #404040
D-pad: border-radius 8px | Actions: border-radius 50%
Gap: 12px between buttons
```

---

## 7. Animations & Interactions

| Interaction | Animation | Duration | Easing |
|-------------|-----------|----------|--------|
| Soft drop | translateY | 100ms | ease-out |
| Hard drop | Instant | — | — |
| Rotation | 90° rotate | 75ms | ease-in-out |
| Horizontal move | translateX | 50ms | ease-out |
| Line clear flash | White flash | 100ms | — |
| Line collapse | translateY down | 200ms | ease-out |
| Score pop | scale 1→1.2→1 | 300ms | ease-out |
| Board shake (game over) | translateX ±4px | 3×50ms | — |
| Overlay fade | opacity 0→1 | 300ms | ease-out |
| Screen transitions | Fade | 300ms | ease |

**Hover:** Buttons 150ms bg transition. Touch controls: instant (no transition).

---

## 8. Responsive Breakpoints

| Breakpoint | Width | Cell | Layout | Touch Controls |
|------------|-------|------|--------|----------------|
| Mobile S | 320px | 14px | Vertical stack | Fixed bottom |
| Mobile M | 375px | 16px | Vertical stack | Fixed bottom |
| Mobile L | 425px | 18px | Vertical stack | Fixed bottom |
| Tablet | 768px | 20px | Side panels | None |
| Desktop | 1024px | 24px | 3-column | None |
| Desktop L | 1440px | 28px | 3-column spacious | None |
| Ultrawide | 2560px | 32px | Centered 960px | None |

---

## 9. Accessibility

- **Keyboard:** Full game playable without mouse. Tab order follows visual hierarchy. Focus: 2px cyan outline, 2px offset.
- **Contrast:** All text meets WCAG 2.1 AA (4.5:1). Piece colors: 7:1+ against #0D0D0D.
- **Colorblind:** Pattern overlays per piece. Toggle in settings.
- **Motion:** Respects `prefers-reduced-motion` — disables rotation animation, line flash, score pop, transitions become instant fades.
- **Touch targets:** All buttons 56×56px (exceeds 44×44px WCAG minimum). 12px gap prevents mis-taps.

---

## 10. Assets & Icons

**Icon library:** Lucide React
- Play: `Play`, Pause: `Pause`, Rotate: `RotateCw`, Hard Drop: `ArrowDownToLine`, Hold: `PanelLeft`, Close: `X`, Settings: `Settings`

**No image assets required** — all visuals are CSS-generated (colors, borders, shadows, SVG patterns).

---

## 11. CSS Design Tokens

```css
:root {
  --color-bg: #0D0D0D;
  --color-surface: #1A1A1A;
  --color-surface-elevated: #262626;
  --color-border: #404040;
  --color-text-primary: #FFFFFF;
  --color-text-secondary: #A3A3A3;
  --color-accent: #00F0F0;
  --color-success: #00F000;
  --color-danger: #F00000;
  --color-i: #00F0F0; --color-o: #F0F000; --color-t: #A000F0;
  --color-s: #00F000; --color-z: #F00000; --color-j: #0000F0;
  --color-l: #F0A000;
  --font-primary: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
  --space-1: 4px; --space-2: 8px; --space-3: 12px; --space-4: 16px;
  --space-6: 24px; --space-8: 32px; --space-12: 48px; --space-16: 64px;
  --radius-sm: 4px; --radius-md: 8px; --radius-full: 9999px;
  --transition-fast: 100ms ease;
  --transition-base: 150ms ease;
  --transition-slow: 300ms ease;
}
```

---

## 12. Design Rationale

- **Dark mode:** Reduces eye strain during extended play; makes colorful pieces pop. #0D0D0D is immersive without being harsh.
- **JetBrains Mono for scores:** Prevents numbers from "dancing" as width changes. Modern, readable, pairs with Inter.
- **No gradients/shadows:** Every pixel serves gameplay. Single 3D highlight on active pieces adds depth without distraction.
- **4px border radius:** Precise enough for grid-based game, modern enough for UI. Sharp 0px corners on board maintain pixel-perfect aesthetic.
- **Cyan accent:** I-piece is the most iconic Tetris piece. Using it for CTAs creates subconscious brand link. Highly visible against dark backgrounds.
- **Touch controls at bottom:** Most comfortable thumb zone on mobile. Allows one-handed play.

---

## Deliverables

1. **Design Spec** (this document) — Complete visual system
2. **Wireframes** — ASCII + HTML wireframes for all 6 screens
3. **High-Fidelity Mockups** — Pixel-perfect HTML/CSS mockups with actual colors, fonts, piece renders, and responsive layouts
4. **Color Palette** — 7 tetromino colors + 7 UI colors + colorblind patterns
5. **Typography Specs** — Full scale with Inter + JetBrains Mono
6. **Responsive Layout** — 6 breakpoints from 320px to 2560px
7. **Design Rationale** — Decision documentation

---

*Design version: 1.0*  
*Author: Diana (UX/UI Designer)*  
*Date: 2026-06-14*
