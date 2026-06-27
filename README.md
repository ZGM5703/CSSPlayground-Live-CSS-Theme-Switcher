# 🎨 CSSPlayground — Live CSS Theme Switcher

An interactive, browser-based CSS showcase built with vanilla HTML, CSS, and JavaScript — no frameworks, no libraries, no dependencies. Click any of the four theme cards to apply a live animated CSS theme to the entire page. Click again to reset.

**🔗 Live demo:** `https://zgm5703.github.io/CSSPlayground-Live-CSS-Theme-Switcher/`

---

## What it does

The homepage displays four theme cards, each previewing a distinct CSS animation style. Clicking a card injects a class onto `<body>` that triggers a complete visual transformation — every element on the page reacts, including the heading, navigation, cards, borders, backgrounds, and buttons. Clicking the same card again removes the theme and resets to the clean default.

---

## How to run it

**Option 1 — Live demo:** Open the GitHub Pages link above directly in any browser.

**Option 2 — Run locally:**
1. Download or clone this repository
2. Open `index.html` in any modern browser
3. That's it — no install, no build step

```bash
git clone https://github.com/ZGM5703/css-playground.git
cd css-playground
open index.html
```

---

## The four themes

### 🌈 Rainbow Rush
The entire page cycles through the color spectrum. The main heading uses a gradient text animation via `background-clip: text`. Card borders cycle through hue independently with staggered `animation-delay`. The background itself shifts through warm tones on a keyframe loop. Nothing is static.

**Key techniques:** `background-clip: text`, `background-size` + `background-position` animation, staggered `animation-delay` via CSS custom properties (`--i`), `hue-rotate`.

---

### 🌸 Breathe
A slow, meditative pulse. The page subtly scales up and down as if it's breathing. Colors shift through soft pastels — lavender, mint, peach — on a 6-second loop. Card shadows and borders shift color in sync, staggered so each card breathes slightly out of phase with the next.

**Key techniques:** `transform: scale()` keyframe animation, staggered delays per card using `calc(var(--i) * 1.2s)`, `box-shadow` color transitions in keyframes.

---

### 💻 Glitch
A terminal green, CRT monitor aesthetic. A `repeating-linear-gradient` scanline pattern is fixed over the entire viewport using a `::before` pseudo-element on `<body>`. The heading uses `::before` and `::after` pseudo-elements with `clip-path: inset()` to create RGB color splitting — red and cyan copies of the text shift and slice at different intervals. The page itself shakes periodically.

**Key techniques:** `clip-path: inset()` on pseudo-elements, `data-text` attribute mirroring, `steps()` timing function, `position: fixed` scanline overlay, `transform: translate()` shake animation.

---

### 🌃 Midnight Rave
A dark mode takeover with two large radial gradient orbs floating behind the content using `position: fixed` pseudo-elements. The heading glows with an animated `text-shadow` cycling through purple, blue, red, and green. Every card and surface has a matching neon glow that cycles in sync using `box-shadow` keyframes. Pills pulse with a colored border glow.

**Key techniques:** `radial-gradient` ambient orbs via `::before`/`::after`, `text-shadow` color animation, `backdrop-filter: blur()` on cards, `box-shadow` with `inset` and outer glow cycling together.

---

## How the theme switching works

The logic is about 20 lines of JavaScript:

```javascript
function applyTheme(key) {
  // Remove all existing theme classes
  Object.values(THEMES).forEach(t => body.classList.remove(t.class));

  // If the same theme is clicked again, reset and exit
  if (current === key) { current = null; return; }

  // Otherwise, add the new theme class to <body>
  body.classList.add(THEMES[key].class);
  current = key;
}
```

All visual work is done purely in CSS. JavaScript only adds or removes a class name on `<body>`. Every animation, color, shadow, and layout change is handled by CSS selectors scoped to that body class, for example:

```css
body.theme-rainbow .hero h1 {
  background: linear-gradient(90deg, #ff6b6b, #ffd43b, #4dabf7 ...);
  -webkit-background-clip: text;
  animation: rainbowText 4s linear infinite;
}
```

---

## Features

- **4 fully distinct animated themes** — each with its own color system, motion language, and personality
- **Whole-page transformation** — every element reacts, not just a single component
- **Toggle behavior** — clicking the active theme again resets to the clean default
- **Active state indicator** — nav badge shows the current theme name
- **Card swatch previews** — each card shows a live miniature preview of its animation before you click
- **Staggered animations** — cards animate out of phase using CSS custom properties (`--i`, `--j`) passed via inline `style`
- **Respects reduced motion** — all animations are disabled for users with `prefers-reduced-motion: reduce`
- **Zero JavaScript animation** — every visual effect is pure CSS keyframes; JS only toggles a class

---

## Technologies used

- HTML5
- CSS3 (custom properties, keyframe animations, pseudo-elements, clip-path, backdrop-filter, gradient text)
- Vanilla JavaScript (class toggling only — ~20 lines total)

---

## What I learned

- Using `body`-level class scoping to build a full theme system without any CSS-in-JS or frameworks
- Creating RGB color split effects with `clip-path: inset()` on `::before` and `::after` pseudo-elements
- Staggering animations across sibling elements using CSS custom properties passed as inline styles
- Building a fixed scanline overlay using `repeating-linear-gradient` on a `position: fixed` pseudo-element
- Using `background-clip: text` with animated `background-position` for smooth gradient text scrolling
- Respecting accessibility with `prefers-reduced-motion` media query

---

## Future improvements

- [ ] Add a 5th theme (e.g. paper texture, retro 8-bit pixel art, or vaporwave)
- [ ] Persist the selected theme to `localStorage` so it survives page refresh
- [ ] Add keyboard navigation (press 1–4 to switch themes)
- [ ] Smooth crossfade transition between themes
- [ ] Theme randomizer button

---

## License

MIT — free to use, modify, and share.
