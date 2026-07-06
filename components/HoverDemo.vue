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
      <code class="mini">onmouseenter / onmouseleave → setState → re-render</code>
      <p class="muted">Extra JS, no keyboard state, and <code>:focus</code> is forgotten.</p>
    </div>

    <div class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ Pure CSS state</span>
      <div class="demo-stage">
        <button class="btn btn--css">Hover / Tab to me</button>
      </div>
      <code class="mini">.btn:hover, .btn:focus-visible { transform: translateY(-4px) }</code>
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
  padding: 0.7rem 1.4rem;
  border-radius: 12px;
  cursor: pointer;
}
.btn--css { transition: transform .2s ease, box-shadow .2s ease; }
.btn--css:hover { transform: translateY(-4px); box-shadow: 0 10px 20px rgba(255,81,44,.35); }
.btn--css:focus-visible { outline: 3px solid var(--th-navy); outline-offset: 3px; }
.mini {
  font-size: 0.72rem; background: #fff; border: 1px solid #e3e7ee;
  border-radius: 6px; padding: 0.35rem 0.5rem; display: block; color: #475569;
}
.muted { font-size: 0.82rem; color: #64748b; margin: 0; }
.muted code { background: #eef1f5; padding: 0 0.25rem; border-radius: 4px; }
</style>
