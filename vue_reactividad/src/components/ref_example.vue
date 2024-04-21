<template>
  <div class="timer">
    <h1>Temporizador con ref</h1>
    <div class="timer_display">{{ formattedTime }}</div>
    <div class="timer_controls">
      <input
        type="number"
        v-model="timeInput"
        min="1"
        step="1"
        placeholder="Tiempo (segundos)"
      />
      <button @click="startTimer" :disabled="timerActive">Iniciar</button>
      <button @click="stopTimer" :disabled="!timerActive">Detener</button>
      <button @click="resetTimer">Reiniciar</button>
    </div>
  </div>
</template>

<script setup>
  import { ref, computed } from 'vue';

  const timeInput = ref(0);
  const timerActive = ref(false);
  let intervalId = null;

  const formattedTime = computed(() => {
    const minutes = Math.floor(timeInput.value / 60);
    const seconds = timeInput.value % 60;
    return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
  });

  const startTimer = () => {
    if (timeInput.value > 0) {
      timerActive.value = true;
      intervalId = setInterval(() => {
        if (timeInput.value > 0) {
          timeInput.value--;
        } else {
          stopTimer();
        }
      }, 1000);
    }
  };

  const stopTimer = () => {
    clearInterval(intervalId);
    timerActive.value = false;
  };

  const resetTimer = () => {
    timeInput.value = 0;
    stopTimer();
  };
</script>

<style scoped>
.timer {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.timer_display {
  font-size: 32px;
  font-weight: bold;
  margin-bottom: 10px;
}

.timer_controls {
  display: flex;
  gap: 10px;
}

input[type="number"] {
  width: 60px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 5px 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}

button:disabled {
  opacity: 0.5;
  cursor: default;
}
</style>
