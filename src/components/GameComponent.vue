<template>
  <div class="game-container">
    <div class="header">
      <h1 class="title">Hangman (PC ONLY)</h1>
      <h2>Can you find the word?</h2>
    </div>
    <div class="game">
      <Figure :wrong-count="wrongLetters.length" />
      <Word :letters="letters" :correct-letters="correctLetters" />
      <WrongLetters :wrong-letters="wrongLetters" />
    </div>
    <Popup :status="status" :word="word" @reset="reset" />
    <Notification :show="notification" />
  </div>
</template>

<script>
import { computed, ref } from "vue";
import Figure from "./FigureComponent.vue";
import WrongLetters from "./WrongLetters.vue";
import Word from "./WordComponent.vue";
import Popup from "./PopupComponent.vue";
import Notification from "./NotificationComponent.vue";
import onKeydown from "@/assets/onKeydown";

const words = [
  "programming",
  "vuejs",
  "composition",
  "javascript",
  "oracle",
  "alura",
  "github",
];
const randomWord = () => words[Math.floor(Math.random() * words.length)];

export default {
  components: { Figure, Word, WrongLetters, Popup, Notification },
  setup() {
    const word = ref(randomWord());
    const guessedLetters = ref([]);
    const letters = computed(() => word.value.split(""));
    const wrongLetters = computed(() =>
      guessedLetters.value.filter((l) => !letters.value.includes(l))
    );
    const correctLetters = computed(() =>
      guessedLetters.value.filter((l) => letters.value.includes(l))
    );
    const status = computed(() => {
      if (wrongLetters.value.length === 6) return "lose";
      if (letters.value.every((l) => correctLetters.value.includes(l)))
        return "win";
      return "";
    });
    const reset = () => {
      guessedLetters.value = [];
      word.value = randomWord();
    };
    const notification = ref(false);
    const showNotification = () => {
      notification.value = true;
      setTimeout(() => (notification.value = false), 2000);
    };
    onKeydown((event) => {
      const letter = event.key.toLowerCase();
      if (event.keyCode < 65 || event.keyCode > 90) return;
      if (status.value) return;
      if (guessedLetters.value.includes(letter)) {
        showNotification();
        return;
      }
      guessedLetters.value.push(letter);
    });
    return {
      letters,
      word,
      wrongLetters,
      correctLetters,
      guessedLetters,
      notification,
      status,
      reset,
    };
  },
};
</script>

<style scoped>
.header {
  color: var(--green);
}

h2 {
  color: white;
  font-size: 1.5rem;
}

.game-container {
  padding-top: 4rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.game {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 4rem;
  height: 100%;
}
</style>
