---
theme: default
title: CSS-First Best Practices
info: Doing more with CSS and less JavaScript — for performance, SEO & maintainability.
fonts:
  sans: Poppins
  weights: "400,500,600,700"
css: unocss
transition: slide-left
mdc: true
layout: cover
---

# CSS-First <em>Best Practices</em>

Doing more with **CSS** and less **JavaScript** — for performance, SEO & maintainability.

<div class="mt-8 text-sm opacity-70">El Mehdi Assamer · Theodo</div>

---
layout: section
---

<div class="th-kicker">The idea</div>

# Why <em>CSS-first?</em>

The browser already knows how to animate, lay out and handle interactions natively.
**CSS-first means using those built-in powers before writing JavaScript** for lighter, faster and more accessible pages.

---
layout: default
---

# What we gain by reaching for CSS first

<div class="th-rule" />

<div class="grid grid-cols-2 gap-6 mt-4">

<div>

### ⚡ Performance

- CSS animations use the **GPU**, so they stay smooth, even while JavaScript is busy
- Less JavaScript means **less to download and run**
- The page feels faster and never freezes

### 🔍 SEO

- Less JavaScript → pages **load faster**
- Faster sites **rank higher** on Google
- Content written in HTML/CSS is **easy for Google to read**

</div>

<div>

### ♿ Accessibility

- Native elements ship keyboard + ARIA **for free**
- `:focus-visible` handles keyboard users correctly

### 🧹 Maintainability

- Fewer dependencies to update & secure
- Declarative, the browser does the work
- Less code to test and debug

</div>

</div>

<div class="th-note mt-4">
<b>The rule of thumb:</b> if the browser can do it natively, don't ship JavaScript for it.
</div>

---
layout: section
---

<div class="th-kicker">6 techniques · live Bad → Good</div>

# What we'll cover

<div class="grid grid-cols-2 gap-x-10 gap-y-1 mt-6 text-lg">

<div>1 · <b>@keyframes & transition</b> vs JS libraries</div>
<div>5 · <b>Flexbox</b> layout</div>
<div>2 · <b>scroll-snap</b> carousel</div>
<div>6 · <b>position: sticky</b></div>
<div>3 · <b>:hover / :focus</b> micro-interactions</div>
<div>4 · <b>&lt;details&gt;</b> native accordion</div>

</div>

---

# 1 · Animations: `@keyframes` over JS libraries

<div class="th-rule" />

<AnimateDemo class="mt-2" />

<div v-click class="th-note">
<b>Best practice:</b> animate <code>transform</code> &amp; <code>opacity</code> in CSS  they run on the GPU/compositor.
Reach for a JS library only for physics, gestures or timeline-orchestrated sequences.
</div>

---

# 2 · `scroll-snap`: a carousel without JavaScript

<div class="th-rule" />

<ScrollSnapDemo class="mt-2" />

<div v-click class="th-note">
<b>Best practice:</b> for sliders &amp; carousels, use <code>scroll-snap-type</code> on the scroller and
<code>scroll-snap-align</code> on each item. The browser snaps to each slide  no carousel library needed.
</div>

---

# 3 · `:hover` / `:focus` micro-interactions

<div class="th-rule" />

<HoverDemo class="mt-2" />

<div v-click class="th-note">
<b>Best practice:</b> express interactive states with CSS pseudo-classes, not JS events.
Always pair <code>:hover</code> with <code>:focus-visible</code> so keyboard users get the same affordance.
</div>

---

# 4 · `<details>`: a native, accessible accordion

<div class="th-rule" />

<DetailsDemo class="mt-2" />

<div v-click class="th-note">
<b>Best practice:</b> use <code>&lt;details&gt;/&lt;summary&gt;</code> for disclosure UI. Open/close, keyboard and ARIA are built in,
and the content stays in the DOM — <b>visible to search engines</b>.
</div>

---

# 5 · Flexbox over manual positioning

<div class="th-rule" />

<LayoutDemo class="mt-2" />

<div v-click class="th-note">
<b>Best practice:</b> use <b>Flexbox</b> for rows &amp; columns. <code>display:flex</code> gives equal-height
columns, <code>gap</code> spaces them, and <code>justify/align</code> centre content no absolute coordinates, no hardcoded heights.
</div>

---

# 6 · `position: sticky` over scroll listeners

<div class="th-rule" />

<StickyDemo class="mt-2" />

<div v-click class="th-note">
<b>Best practice:</b> pin headers, sidebars and section labels with <code>position: sticky; top: 0</code>.
No scroll listeners, no layout thrash the browser handles it on the compositor.
</div>

---

# Bonus · Good CSS habits

<div class="th-rule" />

<div class="bonus-grid grid grid-cols-2 gap-x-8 gap-y-1 mt-3 text-sm">

<div>

**🎨 Use variables for your design tokens** — change a colour once, everywhere updates.

```css
:root { --brand: #ff512c; }
.btn  { background: var(--brand); }
```

**📏 Prefer relative units** — scales & stays accessible.

```css
font-size: clamp(1rem, 2.5vw, 1.5rem); /* not 24px */
```

**🧱 Space with `gap`, not margins** — no fragile margin hacks.

```css
.list { display: flex; gap: 12px; }
```

</div>

<div>

**🚫 Avoid `!important`** — lower specificity instead.

```css
.title { color: red !important; } /* ✗ */
.card .title { color: red; }      /* ✓ */
```

**🪜 Keep selectors shallow** — deep nesting is brittle.

```css
.nav ul li a span { }  /* ✗ */
.nav-link { }          /* ✓ */
```

**♿ Respect user settings** — wrap motion in a media query.

```css
@media (prefers-reduced-motion: reduce) {
  * { animation: none; transition: none; }
}
```

</div>

</div>

<div class="th-note mt-2">
<b>Golden rule:</b> write the simplest CSS that works, the browser is smarter than you think.
</div>

---
layout: section
---

<div class="th-kicker">Takeaways</div>

# Reach for the platform <em>first</em>

<div class="mt-4 text-lg leading-relaxed" style="color:var(--th-light)">

1. **Animate** with `@keyframes` / `transition` on `transform` & `opacity`
2. **Carousels** → `scroll-snap`, not a JS library
3. **State** belongs in `:hover` / `:focus-visible`, not JS events
4. **Disclosure UI** → native `<details>`
5. **Layout** → Flexbox, not floats
6. **Pinning** → `position: sticky`

</div>

<div class="th-note mt-6" style="background:rgba(255,81,44,.12)">
Less JavaScript → faster pages → better SEO → happier users. <b>That's the win.</b>
</div>

---
layout: cover
---

# Thank you 🧡
