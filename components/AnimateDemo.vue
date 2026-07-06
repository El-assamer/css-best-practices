<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const jsX = ref(0)
let raf, dir = 1, t = 0
const tick = () => {
  // Animating `left` in JS forces layout + paint on the main thread every frame
  t += dir * 1.4
  if (t > 100 || t < 0) dir *= -1
  jsX.value = t
  raf = requestAnimationFrame(tick)
}
onMounted(() => { raf = requestAnimationFrame(tick) })
onUnmounted(() => cancelAnimationFrame(raf))
</script>

<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ JS animation library</span>
      <div class="track">
        <div class="ball ball--js" :style="{ left: jsX + '%' }"></div>
      </div>
      <code class="mini">requestAnimationFrame(() =&gt; el.style.left = x + '%')</code>
      <p class="muted">Runs on the main thread · animates <code>left</code> → layout + paint every frame · ships a JS bundle</p>
    </div>

    <div class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ Pure CSS</span>
      <div class="track">
        <div class="ball ball--css"></div>
      </div>
      <code class="mini">@keyframes slide { to { transform: translateX(100%) } }</code>
      <p class="muted">Runs on the compositor thread · animates <code>transform</code> → no layout · 0&nbsp;KB JS</p>
    </div>
  </div>
</template>

<style scoped>
.track {
  position: relative;
  height: 46px;
  background: #fff;
  border: 1px solid #e3e7ee;
  border-radius: 10px;
}
.ball {
  position: absolute;
  top: 50%;
  width: 30px; height: 30px;
  margin-top: -15px;
  border-radius: 50%;
  background: var(--th-coral);
}
.ball--js { transform: translateX(-50%); }
.ball--css {
  left: 0;
  animation: slideXsafe 2.4s ease-in-out infinite alternate;
}
@keyframes slideXsafe {
  from { left: 0; transform: translateX(0); }
  to   { left: 100%; transform: translateX(-100%); }
}
.mini {
  font-size: 0.72rem;
  background: #fff;
  border: 1px solid #e3e7ee;
  border-radius: 6px;
  padding: 0.35rem 0.5rem;
  display: block;
  color: #475569;
}
.muted { font-size: 0.82rem; color: #64748b; margin: 0; }
.muted code { background: #eef1f5; padding: 0 0.25rem; border-radius: 4px; }
</style>
