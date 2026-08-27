<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ JS carousel library</span>
      <div class="rail rail--bad">
        <div class="slide" v-for="n in 5" :key="n">{{ n }}</div>
      </div>
      <pre class="mini">.rail--bad { display: flex; overflow-x: auto; }

/* stops mid-slide → you reach for a library */
import Swiper from 'swiper'
new Swiper('.rail', {
  slidesPerView: 'auto',
  centeredSlides: true,
  // + CSS bundle, breakpoints, event wiring…
})</pre>
      <p class="muted">Free-scrolls and stops <b>mid-slide</b> unless JavaScript forces the snap. Extra bundle.</p>
    </div>

    <div v-click class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ CSS scroll-snap</span>
      <div class="rail rail--good">
        <div class="slide" v-for="n in 5" :key="n">{{ n }}</div>
      </div>
      <pre class="mini">.rail--good {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  scroll-behavior: smooth;
}
.rail--good .slide { scroll-snap-align: center; }</pre>
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
  height: 44px;
  border-radius: 8px;
  display: grid;
  place-items: center;
  font-weight: 700;
  color: #fff;
  background: var(--th-coral);
}
.rail--good .slide { scroll-snap-align: center; }
.mini {
  font-size: 0.62rem; line-height: 1.45; background: #fff; border: 1px solid #e3e7ee;
  border-radius: 6px; padding: 0.4rem 0.55rem; display: block; color: #475569;
  margin: 0; white-space: pre; overflow: auto; max-height: 180px;
}
.muted { font-size: 0.7rem; color: #64748b; margin: 0; }
.muted b { color: inherit; }
</style>
