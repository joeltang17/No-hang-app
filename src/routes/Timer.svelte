<script>
  let timerOn = false;
  let Timer = 60; // Set the initial time in seconds
  let intervalId; // Declare intervalId outside the function

  const start = () => {
    if (!timerOn) {
      // Start the timer
      timerOn = true;
      intervalId = setInterval(() => {
        Timer--;
        if (Timer < 0) {
          clearInterval(intervalId); // Stop the timer when it reaches 0
          timerOn = false;
        }
      }, 1000);
    } else {
      // Pause the timer
      clearInterval(intervalId);
      timerOn = false;
    }
  };

  const reset = () => {
    clearInterval(intervalId);
    timerOn = false;
    Timer = 60; // Reset the timer to the initial time
  };
</script>

<div class="d-flex align-items-center justify-content-center">
  {Timer}
</div>

<div class="d-flex align-items-center justify-content-center">
    <button on:click={start} type="button" class="btn btn-primary">{timerOn ? "Pause" : "Start"}</button>
    <button on:click={reset} type="button" class="btn btn-secondary">Reset</button>
</div>

