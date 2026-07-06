<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ JS carousel library</span>
      <div class="rail rail--bad">
        <div class="slide" v-for="n in 5" :key="n">{{ n }}</div>
      </div>
      <code class="mini">import Swiper from 'swiper'  // + config + JS to snap</code>
      <p class="muted">Free-scrolls and stops <b>mid-slide</b> unless JavaScript forces the snap. Extra bundle.</p>
    </div>

    <div class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ CSS scroll-snap</span>
      <div class="rail rail--good">
        <div class="slide" v-for="n in 5" :key="n">{{ n }}</div>
      </div>
      <code class="mini">scroll-snap-type: x mandatory · scroll-snap-align: center</code>
      <p class="muted">Drag/scroll → the browser <b>snaps to each slide</b>. Zero JavaScript.</p>
    </div>
  </div>
</template>

<style scoped>
.rail {
  display: flex;
  gap: 0.6rem;
  overflow-x: auto;
  padding: 0.4rem;
  background: #fff;
  border: 1px solid #e3e7ee;
  border-radius: 10px;
  scrollbar-width: thin;
}
.rail--good {
  scroll-snap-type: x mandatory;
  scroll-behavior: smooth;
}
.slide {
  flex: 0 0 70%;
  height: 70px;
  border-radius: 8px;
  display: grid;
  place-items: center;
  font-weight: 700;
  color: #fff;
  background: var(--th-coral);
}
.rail--good .slide { scroll-snap-align: center; }
.mini {
  font-size: 0.72rem; background: #fff; border: 1px solid #e3e7ee;
  border-radius: 6px; padding: 0.35rem 0.5rem; display: block; color: #475569;
}
.muted { font-size: 0.82rem; color: #64748b; margin: 0; }
.muted b { color: inherit; }
</style>
