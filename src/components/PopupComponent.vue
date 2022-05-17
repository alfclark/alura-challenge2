<template>
  <div v-if="finalMessage" class="popup-container" id="popup-container">
    <div class="popup">
      <h2>{{ finalMessage }}</h2>
      <h3 v-show="status === 'lose'">...the word was: {{ word }}</h3>
      <button @click="reset">Play Again</button>
    </div>
  </div>
</template>

<script>
import { computed } from "vue";
export default {
  props: {
    status: { type: String, default: "" },
    word: { type: String, default: "" },
  },
  setup(props, { emit }) {
    const finalMessage = computed(() => {
      if (props.status === "win") return "Congratulations! You won! 😃";
      if (props.status === "lose") return "Unfortunately you lost. 😕";
      return "";
    });
    const reset = () => emit("reset");
    return { finalMessage, reset };
  },
};
</script>

<style scoped>
.popup-container {
  background-color: rgba(0, 0, 0, 0.3);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  /* display: none; */
  align-items: center;
  justify-content: center;
}

.popup {
  background-color: rgb(0, 0, 0);
  box-shadow: 0 15px 10px 3px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: center;
  color: var(--green);
}
.popup button {
  cursor: pointer;
  background-color: var(--green);
  color: white;
  border: 0;
  margin-top: 20px;
  padding: 15px 32px;
  font-size: 16px;
  cursor: pointer;
}

.popup button:hover {
  background-color: grey;
  transition: 0.5s;
  transform: scale(1.1);
  color: black;
}

.popup button:focus {
  outline: 0;
}
</style>
