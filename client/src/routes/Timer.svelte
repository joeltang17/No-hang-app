<script>
  let timerOn = false;
  let Timer = 3; // Set the initial time in seconds
  let intervalId;
  let timeoutId; 
  let time = [3, 2]
  const intervals = time.length;
  let i = 0;
  let currTime; 

  const start = (i, newTime) => {
    if(newTime){
      Timer = time[i];
    }
    if (!timerOn) {
      if(i === intervals - 1){
        console.log('l')
        timerOn = true;
        intervalId = setInterval(() => {
        Timer--;
        if (Timer < 1) {
          clearInterval(intervalId);
          timerOn = false;
        }
        }, 1000);
      } 
      else {
        console.log('a')
        timerOn = true;
        
        intervalId = setInterval(() => {
        Timer--;
        if (Timer < 1) {
          clearInterval(intervalId);
          timerOn = false;
        }
        }, 1000);
        timeoutId = setTimeout(() => {start(i+1, true); console.log('p')}, Timer * 1000 + 1)
      }

    } 
    else {
      clearTimeout(timeoutId)
      clearInterval(intervalId);
      timerOn = false;
    }
  };

  const reset = () => {
    clearInterval(intervalId);
    clearTimeout(timeoutId);
    timerOn = false;
    Timer = 3; // Reset the timer to the initial time
  };
</script>

<div class="d-flex align-items-center justify-content-center">
  {Timer}
</div>

<div class="d-flex align-items-center justify-content-center">
    <button on:click={() => start(i, true)} type="button" class="btn btn-primary">{timerOn ? "Pause" : "Start"}</button>
    <button on:click={reset} type="button" class="btn btn-secondary">Reset</button>
</div>

