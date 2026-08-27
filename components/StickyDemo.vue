<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ JS scroll listener → position: fixed</span>
      <div class="scroll-box">
        <div class="bad-head">Header (toggled by JS)</div>
        <p v-for="n in 8" :key="n">Scroll line {{ n }} — the handler fires on every scroll event.</p>
      </div>
      <pre class="mini">window.addEventListener('scroll', () =&gt; {
  if (window.scrollY &gt; header.offsetTop) {
    header.classList.add('is-fixed')    /* position: fixed */
  } else {
    header.classList.remove('is-fixed')
  }
})</pre>
      <p class="muted">Fires constantly, causes layout thrash &amp; jank, needs debouncing.</p>
    </div>

    <div v-click class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ position: sticky</span>
      <div class="scroll-box">
        <div class="good-head">Header (sticky)</div>
        <p v-for="n in 8" :key="n">Scroll line {{ n }} — the browser pins it natively.</p>
      </div>
      <pre class="mini">.header {
  position: sticky;
  top: 0;
}</pre>
      <p class="muted">No listeners, no JS, buttery-smooth — handled by the compositor.</p>
    </div>
  </div>
</template>

<style scoped>
.scroll-box {
  height: 110px; overflow-y: auto;
  background: #fff; border: 1px solid #e3e7ee; border-radius: 10px;
  padding: 0 0.8rem 0.8rem;
}
.scroll-box p { font-size: 0.8rem; color: #475569; margin: 0.5rem 0; }
.bad-head, .good-head {
  font-weight: 600; padding: 0.5rem 0.4rem; font-size: 0.85rem;
  background: #fff;
}
.good-head { position: sticky; top: 0; color: #15803d; border-bottom: 2px solid #b6ecca; }
.bad-head { color: #c8341a; border-bottom: 2px solid #ffc6b8; }
.mini {
  font-size: 0.62rem; line-height: 1.45; background: #fff; border: 1px solid #e3e7ee;
  border-radius: 6px; padding: 0.4rem 0.55rem; display: block; color: #475569;
  margin: 0; white-space: pre; overflow: auto; max-height: 180px;
}
.muted { font-size: 0.7rem; color: #64748b; margin: 0; }
.muted code { background: #eef1f5; padding: 0 0.25rem; border-radius: 4px; }
</style>
