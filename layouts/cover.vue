<template>
  <div class="th-cover">
    <img class="th-cover__wave" src="/theodo-wave.png" alt="" />
    <img class="th-cover__logo" src="/theodo-logo-white.png" alt="theodo" />
    <div class="th-cover__body">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.th-cover {
  position: absolute;
  inset: 0;
  background: var(--th-navy);
  color: #fff;
  padding: 3.5rem 4rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
}
.th-cover__wave {
  position: absolute;
  right: -6%;
  top: 50%;
  transform: translateY(-50%);
  width: 58%;
  opacity: 0.9;
  pointer-events: none;
}
.th-cover__logo {
  position: absolute;
  top: 3rem;
  left: 4rem;
  width: 150px;
}
.th-cover__body { position: relative; max-width: 64%; }
.th-cover__body :deep(h1) {
  color: #fff;
  font-size: 3.1rem;
  line-height: 1.05;
  margin: 0 0 0.6rem;
}
.th-cover__body :deep(h1 em) { color: var(--th-coral); font-style: normal; }
.th-cover__body :deep(p) { color: var(--th-light); font-size: 1.15rem; }
</style>
