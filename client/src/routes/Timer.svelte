<script>
  let timerOn = false;
  let time = [{sec: 3, type: 'crimp'}, {sec: 2, type: 'rest'}]
  let currTimer = time[0].sec;
  let currType = time[0].type; 
  let intervalId;
  let timeoutId; 
  const intervals = time.length;
  let i = 0;

  const start = (newTime) => {
    console.log(i)
    if(newTime){
      console.log('new time')
      currTimer = time[i].sec;
      currType = time[i].type;
    } 
    if (!timerOn) {
      timerOn = true;
      if(i === intervals - 1){
        console.log('last number')

        intervalId = setInterval(() => {
        currTimer--;
        if (currTimer < 1) {
          console.log('finish')
          reset();
        }
        }, 1000);

      } 
      else {
        console.log('not last number')

        intervalId = setInterval(() => {
        currTimer--;
        if (currTimer < 1) {
          clearInterval(intervalId);
          timerOn = false;
        }
        }, 1000);
        timeoutId = setTimeout(() => {i = i + 1; start(true);}, currTimer * 1000 + 1)
      }

    } 
    else {
      console.log('paused')
      clearTimeout(timeoutId);  
      clearInterval(intervalId);
      timerOn = false;
    }
  };

  const reset = () => {
    console.log('reset')
    i = 0;
    clearInterval(intervalId);
    clearTimeout(timeoutId);
    timerOn = false;
    currTimer = time[0].sec;
    currType = time[i].type; 
  };
</script>

<div class="d-flex align-items-center justify-content-center">
  {currTimer}
</div>

<div class="d-flex align-items-center justify-content-center">
  {currType}
</div>


<div class="d-flex align-items-center justify-content-center">
    <button on:click={() => start(false)} type="button" class="btn btn-primary">{timerOn ? "Pause" : "Start"}</button>
    <button on:click={reset} type="button" class="btn btn-secondary">Reset</button>
</div>

