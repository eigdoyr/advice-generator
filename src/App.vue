<template>
  <main>
    <div class="card">
      <h1 class="advice-number">
        advice &num; <span>{{ slip.id }}</span>
      </h1>
      <p id="advice-text" class="advice-text">
        &ldquo;{{ slip.advice }}&rdquo;
      </p>
      <div class="card-divider"></div>
      <button @click="showAdvice()" type="button" class="dice">
        <img src="../src/assets/icon-dice.svg" alt="dice" />
      </button>
    </div>
  </main>
</template>

<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";

const slip = ref("loading");

const showAdvice = async () => {
  try {
    const response = await axios.get("https://api.adviceslip.com/advice");
    slip.value = response.data.slip;
  } catch (err) {
    console.log(err);
  }
};

onMounted(showAdvice);
</script>

<style scoped>
main {
  display: grid;
  place-content: center;
  min-height: 100vh;
  background-color: var(--main-bg);
}

.card {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  text-align: center;
  background-color: var(--card-bg);
  padding: 2rem;
  margin: 0.75rem;
  height: 20rem;
  border-radius: 0.8rem;
  max-width: 33.8125rem;
  box-shadow: rgba(14, 13, 13, 0.733) 5.95px 5.95px 10px;
}

.advice-number {
  color: var(--accent);
  text-transform: uppercase;
  font-size: 0.65rem;
  letter-spacing: 0.2rem;
  animation: fadeIn 3s;
}

.advice-text {
  color: var(--primary);
  font-size: 1.5rem;
  animation: fadeIn 3s;
  background: -webkit-linear-gradient(360deg, #00ffa0 0%, #ffffff 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.card-divider {
  content: url("../src/assets/pattern-divider-mobile.svg");
  margin-bottom: 4vh;
  transition: all 0.3s ease-in;
}

button {
  all: unset; /** remove all default style **/
}
.dice {
  position: absolute;
  bottom: -2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--accent);
  width: 4rem;
  height: 4rem;
  border-radius: 50%;
  animation: rollIn 0.8s;
  box-shadow: rgba(14, 13, 13, 0.733) 5.95px 5.95px 10px;
}

.dice:hover {
  box-shadow: 0 3px 40px var(--accent);
  transition: all 0.2s linear;
  cursor: pointer;
  transform: scale(1.05);
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes rollIn {
  0% {
    opacity: 0;
    transform: translateX(-10%) rotate(-120deg);
  }
  100% {
    opacity: 1;
    transform: translateX(0px) rotate(0deg);
  }
}

@media (width<375px) {
  .card-divider {
    content: none;
  }

  .advice-text {
    font-size: 1rem;
  }
}

@media (width>=35.3125rem) {
  .card {
    height: 20.95rem;
    width: 33.8125rem;
    padding: 2.85rem;
  }

  .advice-number {
    font-size: 0.75rem;
  }
  .advice-text {
    font-size: 1.6rem;
  }
  .card-divider {
    content: url("../src/assets/pattern-divider-desktop.svg");
    margin-bottom: 3.5vh;
  }
}
</style>
