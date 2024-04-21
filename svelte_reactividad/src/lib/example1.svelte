<script>
  let chosenTime = 10;
  let remainingTime = chosenTime; 
  let interval;

  function startTimer() {
    clearInterval(interval); 
    remainingTime = chosenTime;
    interval = setInterval(() => {
      if (remainingTime > 0) {
        remainingTime--;
      } else {
        clearInterval(interval);
      }
    }, 1000);
  }

  function resetTimer() {
    clearInterval(interval); 
    remainingTime = chosenTime;
  }
  </script>
  
  <h1>Temporizador en svelte</h1>
  <div>
    <p>Segundos restantes: {remainingTime}</p>
    <label>
      Elija el tiempo (en segundos):
      <input type="number" bind:value={chosenTime}>
    </label>
    <br>
    <button on:click={startTimer}>Iniciar Temporizador</button>
    <button on:click={resetTimer}>Reiniciar Temporizador</button>
  </div>
  