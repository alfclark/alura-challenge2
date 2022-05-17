<template>
  <div class="wrong-letters-container">
    <div class="wrong-letters">
      <p v-show="wrongLetters.length > 0">Wrong</p>
      <span v-for="(letter, i) in wrongLetters" :key="letter">
        {{ letter }}
        {{ i === wrongLetters.length - 1 ? "" : ", " }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    wrongLetters: { type: Array, default: () => [] },
  },
};
</script>

<style scoped>
.wrong-letters-container {
  color: var(--red);
  display: flex;
  flex-direction: column;
  text-align: center;
}
.wrong-letters-container p {
  margin: 1rem 0 0 0;
}

.wrong-letters-container span {
  font-size: 1rem;
}
</style>
