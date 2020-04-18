<template>
  <main>
  <back-soon />
  <div class="zeugs">
    <small>
      Elektronische Signaturen und digitales Vertrauen sind brandaktuelle Themen. Wegen Unterhaltsarbeiten bei Swisscom ist der VideoIdent Service temporär offline. Bitte probieren Sie es später nochmals.
    </small>
  </div>
</main>
</template>

<script lang="ts">
import BackSoon from '~/components/BackSoon.vue'

// @ts-ignore
export default {
  components: {
    BackSoon,
  },
}
</script>

<style scoped>
body {
  font: bold 20px/1 Arial;
  color: #60718e;
}

main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
}

img {
  width: 414px;
  max-width: 90%;
}

.zeugs {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 28px 20px;
}

ul {
  list-style-type: none;
}

small {
  max-width: 420px;
  text-align: center;
  font: 12px/1.2 Arial;
}

small a {
  display: inline;
  text-decoration: underline;
  color: #60718e;
}
</style>
