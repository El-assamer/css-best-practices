<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ position: absolute + manual offsets</span>
      <div class="row-bad">
        <div class="col col--bad">Short</div>
        <div class="col col--bad">A bit more text in this column</div>
        <div class="col col--bad">Tiny</div>
      </div>
      <pre class="mini">.row { position: relative; height: 40px; /* hardcoded */ }
.col { position: absolute; top: 4px; width: 32%; }
.col:nth-of-type(1) { left: 4px; }
.col:nth-of-type(2) { left: 0; margin-left: 34%; }
.col:nth-of-type(3) { right: 4px; }</pre>
      <p class="muted">Out of flow → parent <b>collapses</b>, so you hardcode a height; positions are <b>manual math</b> and content overflows.</p>
    </div>

    <div v-click class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ display: flex</span>
      <div class="row-good">
        <div class="col col--good">Short</div>
        <div class="col col--good">A bit more text in this column</div>
        <div class="col col--good">Tiny</div>
      </div>
      <pre class="mini">.row { display: flex; gap: .6rem; }
.col { flex: 1; }</pre>
      <p class="muted"><b>Equal heights</b> automatically, even spacing with <code>gap</code>, no clearfix.</p>
    </div>
  </div>
</template>

<style scoped>
/* BAD: absolute positioning — children leave the flow, so the parent
   collapses and you must hardcode a height + every coordinate by hand */
.row-bad {
  position: relative; height: 40px;   /* must hardcode: children are out of flow */
  background: #fff; border: 1px solid #e3e7ee; border-radius: 10px;
}
.col--bad {
  position: absolute; top: 4px; width: 32%; box-sizing: border-box;
  background: #ffe1d8; border: 1px solid #ffc6b8; color: #c8341a;
  overflow: hidden; white-space: nowrap; text-overflow: ellipsis;
}
.col--bad:nth-of-type(1) { left: 4px; }                 /* pin to the left  */
.col--bad:nth-of-type(2) { left: 0; margin-left: 34%; } /* offset by hand   */
.col--bad:nth-of-type(3) { right: 4px; }                /* pin to the right */

/* GOOD: flex — all columns stretch to the tallest by default */
.row-good {
  display: flex; gap: 0.6rem;
  background: #fff; border: 1px solid #e3e7ee; border-radius: 10px; padding: 0.5rem;
}
.col--good { flex: 1; background: #d6f5e3; border: 1px solid #b6ecca; color: #15803d; }

.col {
  border-radius: 6px; padding: 0.5rem; font-size: 0.8rem; font-weight: 600;
}
.mini {
  font-size: 0.62rem; line-height: 1.45; background: #fff; border: 1px solid #e3e7ee;
  border-radius: 6px; padding: 0.4rem 0.55rem; display: block; color: #475569;
  margin: 0; white-space: pre; overflow: auto; max-height: 180px;
}
.muted { font-size: 0.7rem; color: #64748b; margin: 0; }
.muted code { background: #eef1f5; padding: 0 0.25rem; border-radius: 4px; }
</style>
