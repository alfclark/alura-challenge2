<template>
  <div class="word">
    <span class="letter" v-for="(letter, i) in letters" :key="i">
      {{ correctLetters.includes(letter) ? letter : "" }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    letters: { type: Array, required: true },
    correctLetters: { type: Array, default: () => [] },
  },
};
</script>

<style scoped>
.word {
  display: flex;
  color: var(--green);
  margin-top: 1rem;
}

.letter {
  border-bottom: 3px solid var(--green);
  display: inline-flex;
  font-size: 30px;
  align-items: center;
  justify-content: center;
  margin: 0 3px;
  height: 50px;
  width: 20px;
}
</style>
