# Components Reference — CSS Used in Each Demo

Every content slide embeds a Vue demo component that shows a **Bad → Good** comparison
side by side. This file documents each component, the technique it demonstrates, and the
**CSS that actually makes it work** (the key rules, not the cosmetic styling).

All components share the same shell defined in `style.css`:

```css
.cmp        { display: grid; grid-template-columns: 1fr 1fr; gap: 1.1rem; }  /* two columns */
.cmp-card--bad  { border-color: #ffd2c7; background: #fff6f3; }  /* red-tinted "bad" card */
.cmp-card--good { border-color: #c6efd6; background: #f3fcf7; }  /* green-tinted "good" card */
.cmp-tag--bad   { color: #c8341a; background: #ffe1d8; }         /* ✗ pill */
.cmp-tag--good  { color: #15803d; background: #d6f5e3; }         /* ✓ pill */
```

Brand tokens (from `style.css` `:root`): `--th-navy: #1d2838`, `--th-coral: #ff512c`,
`--th-light: #e9ebef`.

---

## 1. `AnimateDemo.vue` — Slide 5 (Animations)

**Shows:** JS animating `left` on the main thread (janky) vs CSS `@keyframes` on the compositor.

**Bad side:** JS uses `requestAnimationFrame` to update `el.style.left` every frame → forces
layout + paint on the main thread.

**Good side — the CSS that matters:**

```css
.ball--css {
  left: 0;
  animation: slideXsafe 2.4s ease-in-out infinite alternate;
}
@keyframes slideXsafe {
  from { left: 0;    transform: translateX(0); }
  to   { left: 100%; transform: translateX(-100%); }
}
```

**Key point for the audience:** the `@keyframes` runs the animation with no JS. In real code
you'd animate `transform` alone (pure compositor); here `left` is paired with a
`translateX` correction just so the ball stays inside the track visually.

---

## 2. `ScrollSnapDemo.vue` — Slide 6 (scroll-snap carousel)

**Shows:** a free-scrolling rail (stops mid-slide) vs a rail that snaps to each slide.

**The CSS that matters:**

```css
.rail {                        /* the scroller */
  display: flex;
  gap: 0.6rem;
  overflow-x: auto;            /* horizontal scroll */
}
.rail--good {
  scroll-snap-type: x mandatory;   /* snap horizontally, always land on a slide */
  scroll-behavior: smooth;
}
.slide {
  flex: 0 0 70%;               /* each slide is 70% wide, doesn't shrink */
}
.rail--good .slide {
  scroll-snap-align: center;   /* snap point = center of each slide */
}
```

**Key point:** `scroll-snap-type` on the container + `scroll-snap-align` on the items = a
carousel with zero JavaScript.

---

## 3. `HoverDemo.vue` — Slide 7 (`:hover` / `:focus`)

**Shows:** a button animated via JS `@mouseenter`/`@mouseleave` (no keyboard state) vs pure CSS.

**The CSS that matters:**

```css
.btn--css { transition: transform .2s ease, box-shadow .2s ease; }

.btn--css:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 20px rgba(255,81,44,.35);
}
.btn--css:focus-visible {           /* keyboard users get the ring, too */
  outline: 3px solid var(--th-navy);
  outline-offset: 3px;
}
```

**Key point:** `:hover` handles mouse, `:focus-visible` handles keyboard — both for free,
no JS events, no re-renders.

---

## 4. `DetailsDemo.vue` — Slide 8 (native `<details>` accordion)

**Shows:** a `<div>` + `v-show` + click handler (JS owns the state) vs native `<details>`.

**The good side is HTML, not JS:**

```html
<details class="acc-native">
  <summary>What is CSS-first?</summary>
  <div class="acc-native__body">Open/close, keyboard, and ARIA are built in…</div>
</details>
```

**CSS just styles the marker (behavior is native):**

```css
.acc-native summary { cursor: pointer; list-style: none; }
.acc-native summary::-webkit-details-marker { display: none; }  /* hide default triangle */
.acc-native summary::after       { content: "+"; color: var(--th-coral); }  /* custom + icon */
.acc-native[open] summary::after { content: "−"; }              /* becomes − when open */
```

**Key point:** open/close, keyboard, and ARIA come from the `<details>` element itself. CSS
only restyles the icon; the `[open]` attribute selector lets us react to the open state
without any JS.

---

## 5. `LayoutDemo.vue` — Slide 9 (Flexbox over floats)

**Shows:** floated columns (uneven heights, needs clearfix) vs flex columns (equal heights).

**Bad side (floats):**

```css
.row-bad::after { content: ''; display: block; clear: both; }  /* clearfix hack */
.col--bad { float: left; width: 32%; margin-right: 2%; }        /* fragile widths */
```

**Good side (flex) — the CSS that matters:**

```css
.row-good {
  display: flex;
  gap: 0.6rem;         /* even spacing, no margin math */
}
.col--good {
  flex: 1;             /* equal widths; all columns stretch to the tallest by default */
}
```

**Key point:** `display: flex` + `flex: 1` gives equal-height, evenly spaced columns with no
floats and no clearfix.

---

## 6. `StickyDemo.vue` — Slide 10 (`position: sticky`)

**Shows:** a header toggled by a JS `scroll` listener (jank) vs a natively pinned header.

**The CSS that matters:**

```css
.scroll-box { height: 150px; overflow-y: auto; }  /* the scroll container */

.good-head {
  position: sticky;   /* pins itself when it reaches the top */
  top: 0;             /* stick at 0px from the top of the scroll container */
}
```

**Key point:** `position: sticky; top: 0` pins the header with no scroll listener. The browser
handles it on the compositor — smooth, no layout thrash.

---

## 7. `ContainerDemo.vue` — Slide 11 (Container Queries)

**Shows:** the same card in a **wide** slot and a **narrow** slot. With a media query it can't
adapt to the narrow slot; with a container query it stacks itself.

**The CSS that matters:**

```css
.cq { container-type: inline-size; }   /* "measure MY width" — makes this a query container */

/* Reacts to the CONTAINER's width, not the screen's */
@container (max-width: 240px) {
  .card--cq {
    flex-direction: column;            /* narrow container → stack vertically */
    align-items: flex-start;
  }
}
```

The narrow wrapper is `width: 175px`, so it triggers the `max-width: 240px` container query
and the card stacks — **even though the screen is wide.** A plain `@media` query keyed to the
screen would never fire here.

**Key point:** `container-type: inline-size` + `@container` = a component that adapts to its
own space, so it works in a sidebar, modal, or full page unchanged.

---

## Shared / reusable CSS (in `style.css`)

Rules reused across several components:

```css
.th-rule { width: 64px; height: 5px; background: var(--th-coral); }  /* coral underline */

.th-note {                             /* the "Best practice" callout box */
  border-left: 4px solid var(--th-coral);
  background: #fff4f0;
}

.demo-stage {                          /* the dashed sandbox some demos sit in */
  background: #f4f6f9;
  border: 1px dashed #cfd6e0;
  display: flex; align-items: center; justify-content: center;
}
```

Each component also defines a local `.mini` (small code caption) and `.muted` (gray helper
text) — purely cosmetic, safe to ignore when explaining the techniques.
