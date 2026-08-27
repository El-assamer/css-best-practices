<script setup>
import { ref } from 'vue'
const hovered = ref(false)
</script>

<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ JS event handlers</span>
      <div class="demo-stage">
        <button
          class="btn"
          :style="{ transform: hovered ? 'translateY(-4px)' : 'none',
                    boxShadow: hovered ? '0 10px 20px rgba(255,81,44,.35)' : 'none' }"
          @mouseenter="hovered = true"
          @mouseleave="hovered = false"
        >Hover me</button>
      </div>
      <pre class="mini">const hovered = ref(false)

&lt;button
  @mouseenter="hovered = true"
  @mouseleave="hovered = false"
  :style="{ transform: hovered ? 'translateY(-4px)' : 'none',
            boxShadow: hovered ? '0 10px 20px …' : 'none' }"&gt;</pre>
      <p class="muted">Extra JS, no keyboard state, and <code>:focus</code> is forgotten.</p>
    </div>

    <div v-click class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ Pure CSS state</span>
      <div class="demo-stage">
        <button class="btn btn--css">Hover / Tab to me</button>
      </div>
      <pre class="mini">.btn--css { transition: transform .2s ease, box-shadow .2s ease; }
.btn--css:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 20px rgba(255, 81, 44, .35);
}
.btn--css:focus-visible { outline: 3px solid var(--th-navy); }</pre>
      <p class="muted">Zero JS · keyboard users get a <code>:focus-visible</code> ring for free.</p>
    </div>
  </div>
</template>

<style scoped>
.btn {
  border: none;
  background: var(--th-coral);
  color: #fff;
  font-weight: 600;
  font-size: 0.8rem;
  padding: 0.5rem 1.1rem;
  border-radius: 12px;
  cursor: pointer;
}
.btn--css { transition: transform .2s ease, box-shadow .2s ease; }
.btn--css:hover { transform: translateY(-4px); box-shadow: 0 10px 20px rgba(255,81,44,.35); }
.btn--css:focus-visible { outline: 3px solid var(--th-navy); outline-offset: 3px; }
.mini {
  font-size: 0.62rem; line-height: 1.45; background: #fff; border: 1px solid #e3e7ee;
  border-radius: 6px; padding: 0.4rem 0.55rem; display: block; color: #475569;
  margin: 0; white-space: pre; overflow: auto; max-height: 180px;
}
.muted { font-size: 0.7rem; color: #64748b; margin: 0; }
.muted code { background: #eef1f5; padding: 0 0.25rem; border-radius: 4px; }
</style>
