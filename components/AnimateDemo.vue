<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const ballLeftPercent = ref(0)
let frameId
let direction = 1
let position = 0

// Animating `left` in JS forces layout + paint on the main thread every frame
const moveBall = () => {
  position += direction * 1.4
  if (position > 100 || position < 0) direction *= -1
  ballLeftPercent.value = position
  frameId = requestAnimationFrame(moveBall)
}
onMounted(() => { frameId = requestAnimationFrame(moveBall) })
onUnmounted(() => cancelAnimationFrame(frameId))
</script>

<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ JS animation library</span>
      <div class="track">
        <div class="ball ball--js" :style="{ left: ballLeftPercent + '%' }"></div>
      </div>
      <pre class="mini">const ballLeftPercent = ref(0)
let frameId, direction = 1, position = 0

const moveBall = () =&gt; {
  position += direction * 1.4
  if (position &gt; 100 || position &lt; 0) direction *= -1
  ballLeftPercent.value = position          // → el.style.left
  frameId = requestAnimationFrame(moveBall)
}
onMounted(() =&gt; { frameId = requestAnimationFrame(moveBall) })
onUnmounted(() =&gt; cancelAnimationFrame(frameId))</pre>
      <p class="muted">Runs on the main thread · animates <code>left</code> → layout + paint every frame · ships a JS bundle</p>
    </div>

    <div v-click class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ Pure CSS</span>
      <div class="track">
        <div class="ball ball--css"></div>
      </div>
      <pre class="mini">.ball--css {
  animation: slideXsafe 1s ease-in-out infinite alternate;
}
@keyframes slideXsafe {
  from { left: 0;    transform: translateX(0); }
  to   { left: 100%; transform: translateX(-100%); }
}</pre>
      <p class="muted">Runs on the compositor thread · animates <code>transform</code> → no layout · 0&nbsp;KB JS</p>
    </div>
  </div>
</template>

<style scoped>
.track {
  position: relative;
  height: 34px;
  background: #fff;
  border: 1px solid #e3e7ee;
  border-radius: 10px;
}
.ball {
  position: absolute;
  top: 50%;
  width: 22px; height: 22px;
  margin-top: -11px;
  border-radius: 50%;
  background: var(--th-coral);
}
.ball--js { transform: translateX(-50%); }
.ball--css {
  left: 0;
  animation: slideXsafe 1s ease-in-out infinite alternate;
}
@keyframes slideXsafe {
  from { left: 0; transform: translateX(0); }
  to   { left: 100%; transform: translateX(-100%); }
}
.mini {
  font-size: 0.6rem;
  line-height: 1.45;
  background: #fff;
  border: 1px solid #e3e7ee;
  border-radius: 6px;
  padding: 0.4rem 0.55rem;
  display: block;
  color: #475569;
  margin: 0;
  white-space: pre;
  overflow: auto;
  max-height: 200px;
}
.muted { font-size: 0.7rem; color: #64748b; margin: 0; }
.muted code { background: #eef1f5; padding: 0 0.25rem; border-radius: 4px; }
</style>
