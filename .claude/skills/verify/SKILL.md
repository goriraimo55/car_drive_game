---
name: verify
description: Verify the car driving game (index.html) by driving it in a headless browser.
---

# Verifying this project

Single-file browser game — no build step, no server needed.

1. Install Playwright in the scratchpad (`npm i playwright --no-save`) and launch
   the pre-installed Chromium: `executablePath: "/opt/pw-browsers/chromium"`.
2. Open `file:///home/user/car_drive_game/index.html`.
3. All game state is on `window` (`state`, `carX`, `stars`, `items`,
   `celebrateTimer`, `speed`) — inspect it via `page.evaluate`.

Flows worth driving:
- Select screen → click a car button (positions from `selectButtons()` in page context) → `state === "play"`.
- Steering: mouse drag and ArrowLeft/ArrowRight both move `carX`; clamped inside `roadRect()`.
- Collection: push an item at the car's position into `items` and check `stars` increments (star/fruit) or `carWobble` triggers (cone, no score change).
- Milestone: set `stars = 9`, collect one → `celebrateTimer > 0` and `speed` increases.
- Screenshot at desktop (800×600) and portrait mobile (400×700) sizes.

Gotcha: capture `pageerror`/console errors — canvas games fail silently otherwise.
