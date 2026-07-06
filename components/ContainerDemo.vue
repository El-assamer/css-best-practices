<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ Viewport media query</span>
      <div class="wide">
        <article class="card card--mq"><div class="thumb"></div><div><b>Wide slot</b><p>OK here</p></div></article>
      </div>
      <div class="narrow">
        <article class="card card--mq"><div class="thumb"></div><div><b>Narrow slot</b><p>still row → cramped</p></div></article>
      </div>
      <code class="mini">@media (max-width: 600px){…}  /* keys off the screen, not the card */</code>
    </div>

    <div class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ @container query</span>
      <div class="wide cq">
        <article class="card card--cq"><div class="thumb"></div><div><b>Wide slot</b><p>row layout</p></div></article>
      </div>
      <div class="narrow cq">
        <article class="card card--cq"><div class="thumb"></div><div><b>Narrow slot</b><p>stacks itself</p></div></article>
      </div>
      <code class="mini">@container (max-width: 240px){ .card{ flex-direction: column } }</code>
    </div>
  </div>
</template>

<style scoped>
.wide, .narrow { background: #f4f6f9; border: 1px dashed #cfd6e0; border-radius: 8px; padding: 0.4rem; margin-bottom: 0.4rem; }
.wide { width: 100%; }
.narrow { width: 175px; }
.cq { container-type: inline-size; }

.card { display: flex; gap: 0.5rem; align-items: center; background: #fff; border: 1px solid #e3e7ee; border-radius: 8px; padding: 0.45rem; }
.card .thumb { width: 34px; height: 34px; border-radius: 6px; background: var(--th-coral); flex: none; }
.card b { font-size: 0.85rem; }
.card p { margin: 0; font-size: 0.72rem; color: #64748b; }

/* GOOD: reacts to the container's own width */
@container (max-width: 240px) {
  .card--cq { flex-direction: column; align-items: flex-start; text-align: left; }
}
.mini {
  margin-top: 0.3rem;
  font-size: 0.68rem; background: #fff; border: 1px solid #e3e7ee;
  border-radius: 6px; padding: 0.35rem 0.5rem; display: block; color: #475569;
}
</style>
