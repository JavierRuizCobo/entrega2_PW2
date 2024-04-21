<script>
  import { onMount, onDestroy } from "svelte";

  let timeInput = 0;
  let timerActive = false;
  let intervalId = null;

  const formattedTime = (time) => {
    const minutes = Math.floor(time / 60);
    const seconds = time % 60;
    return `${minutes.toString().padStart(2, "0")}:${seconds
      .toString()
      .padStart(2, "0")}`;
  };

  const startTimer = () => {
    if (timeInput > 0) {
      timerActive = true;
      intervalId = setInterval(() => {
        if (timeInput > 0) {
          timeInput--;
        } else {
          stopTimer();
        }
      }, 1000);
    }
  };

  const stopTimer = () => {
    clearInterval(intervalId);
    timerActive = false;
  };

  const resetTimer = () => {
    timeInput = 0;
    stopTimer();
  };

  let formattedTimeString = formattedTime(timeInput);

  $: {
    formattedTimeString = formattedTime(timeInput);
  }

  onMount(() => {
    return () => clearInterval(intervalId);
  });

  onDestroy(() => {
    clearInterval(intervalId);
  });
</script>

<div class="timer">
  <h1>Temporizador con svelte</h1>
  <div class="timer_display">{formattedTimeString}</div>
  <div class="timer_controls">
    <input
      type="number"
      bind:value={timeInput}
      min="1"
      step="1"
      placeholder="Tiempo (segundos)"
    />
    <button on:click={startTimer} disabled={timerActive}>Iniciar</button>
    <button on:click={stopTimer} disabled={!timerActive}>Detener</button>
    <button on:click={resetTimer}>Reiniciar</button>
  </div>
</div>

<style>
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
