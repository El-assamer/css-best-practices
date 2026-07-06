<template>
  <div class="th-section">
    <img class="th-section__logo" src="/theodo-logo-white.png" alt="theodo" />
    <div class="th-section__body">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.th-section {
  position: absolute;
  inset: 0;
  background: var(--th-navy);
  color: #fff;
  padding: 4rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.th-section::before {
  content: '';
  position: absolute;
  left: 0; top: 0; bottom: 0;
  width: 10px;
  background: var(--th-coral);
}
.th-section__logo { position: absolute; top: 3rem; right: 4rem; width: 110px; opacity: 0.85; }
.th-section__body :deep(h1) { color: #fff; font-size: 2.6rem; margin: 0; }
.th-section__body :deep(h1 em) { color: var(--th-coral); font-style: normal; }
.th-section__body :deep(p) { color: var(--th-light); font-size: 1.1rem; margin-top: 0.6rem; }
.th-section__body :deep(.th-kicker) {
  color: var(--th-coral); font-weight: 600; letter-spacing: 0.12em;
  text-transform: uppercase; font-size: 0.85rem;
}
</style>
