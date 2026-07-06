<script setup>
import { ref } from "vue";
const open = ref(false);
</script>

<template>
  <div class="cmp">
    <div class="cmp-card cmp-card--bad">
      <span class="cmp-tag cmp-tag--bad">✗ div + JS click handler</span>
      <div class="acc">
        <div class="acc__head" @click="open = !open">
          What is CSS-first? <span>{{ open ? "−" : "+" }}</span>
        </div>
        <div class="acc__body" v-show="open">
          Hidden with <code>v-show</code> → JS owns the state, no built-in
          keyboard support, screen-reader needs manual ARIA.
        </div>
      </div>
      <code class="mini"
        >&lt;div onclick&gt; + useState + aria-expanded + role…</code
      >
    </div>

    <div class="cmp-card cmp-card--good">
      <span class="cmp-tag cmp-tag--good">✓ Native &lt;details&gt;</span>
      <details class="acc-native">
        <summary>What is CSS-first?</summary>
        <div class="acc-native__body">
          Open/close, keyboard, and ARIA are <b>built in</b>. Content stays in
          the DOM → crawlable &amp; <b>SEO-friendly</b>.
        </div>
      </details>
      <code class="mini"
        >&lt;details&gt;&lt;summary&gt;…&lt;/summary&gt; …
        &lt;/details&gt;</code
      >
    </div>
  </div>
</template>

<style scoped>
.acc,
.acc-native {
  background: #fff;
  border: 1px solid #e3e7ee;
  border-radius: 10px;
  overflow: hidden;
}
.acc__head,
.acc-native summary {
  padding: 0.7rem 0.9rem;
  font-weight: 600;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  list-style: none;
}
.acc-native summary::-webkit-details-marker {
  display: none;
}
.acc-native summary::after {
  content: "+";
  color: var(--th-coral);
  font-weight: 700;
}
.acc-native[open] summary::after {
  content: "−";
}
.acc__body,
.acc-native__body {
  padding: 0.7rem 0.9rem;
  border-top: 1px solid #eef1f5;
  font-size: 0.85rem;
  color: #475569;
}
.acc__body code,
.acc-native__body {
}
.mini {
  margin-top: 0.6rem;
  font-size: 0.72rem;
  background: #fff;
  border: 1px solid #e3e7ee;
  border-radius: 6px;
  padding: 0.35rem 0.5rem;
  display: block;
  color: #475569;
}
code {
  background: #eef1f5;
  padding: 0 0.25rem;
  border-radius: 4px;
}
</style>
