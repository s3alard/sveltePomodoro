<style>
  *{
    margin: 0;
    padding: 0;
    font-family:
    sans-serif;
    box-sizing:border-box;
 }
 
 #black-outline {
     border-radius: 50%;
     position:relative;
     width: 400px;
     height: 400px;
     background-color:white;
     text-align:center;
     line-height: 400px;
     margin-left:  auto;
     margin-right: auto;
     align-self: center;
     z-index:1; 
 }
 
 #main-box { 
     position:absolute;
     left:5px;
     top:5px;
     width:390px;
     height:390px;
     color:black;
     background-color:white;
     border-radius: 50%;
     font-size: 35px;
     text-align:center;
     line-height: 400px;
     margin-left:  auto;
     margin-right: auto;
     align-self: center;
     z-index: 6;
 }
 
 .box-name {
     position:static;
     margin-top: -50px;
 }
 
 .big-time-display {
     position:absolute;
     left:50%;
     transform: translateX(-50%);
     top:40px;
 }
 
 .start-and-reset {
     margin-left: auto;
     margin-right: auto;
     text-align: center;
 }
 
 .left-button {
     position:static;
     left:20px;
     bottom:20px;
     width:60px;
     height: 60px;
     color:black;
     background:white;
     border: 5px solid black;
     font-size: 17px;
     margin-right: 30px;
 
 }
 
 .left-button:hover , .right-button:hover {
     border: 5px solid red;
 }
 
 .right-button {
     position:static;
     right:20px;
     bottom:20px;
     width:60px;
     height: 60px;
     color:rgb(119, 102, 102);
     background:white;
     border: 5px solid black;
     font-size: 17px;
     margin-left: 30px;
 }
 
 .settings {
     width:100%;
     height:auto;
     display: flex;
     justify-content:center;
 
     margin-left: auto;
     margin-right: auto;
 }
 
 .box {
     position:relative;
     width: 200px;
     height:200px;
     background:white;
     color:black;
     border:5px solid black;
     font-size :25px;
     text-align:center;
     line-height: 200px;
     margin:10px;
     padding:10px;
 }
 
 .small-time-display {
     position:absolute;
     left:50%;
     transform: translateX(-50%);
     top:10px;
 }
 
 .minus-button {
     position:absolute;
     left:20%;
     bottom:20%;
     width:30px;
     height: 30px;
     color:white;
     background:black;
     border-radius: 50%;
     font-size: 17px;
     margin-right: 30px;   
     margin-bottom: -10px;
 }
 
 .plus-button {
     position:absolute;
     right:20%;
     bottom:20%;
     width:30px;
     height: 30px;
     color:white;
     background:black;
     border-radius: 50%;
     font-size: 17px;
     margin-left: 30px;
     margin-bottom: -10px;
 }
</style>

<script lang="ts">
  let currentPhase: string = "pomodoro 1";
  let mainDisplay: string = "25:00";
  let pomodoroDisplay: string = "25:00";
  let shortBreakDisplay: string = "05:00";
  let longBreakDisplay: string = "25:00";

  let timeInterval: number = 0;


 // let pomodoroTime: number = 1500;
//  let pomodoroTimerTime: number = pomodoroTime;
 // let shortBreakTime: number = 300;
 // let shortBreakTimerTime: number = shortBreakTime;
 // let longBreakTime: number = 1500;
 // let longBreakTimerTime: number = longBreakTime;
//debugnumbers//
  let pomodoroTime: number = 10;
  let pomodoroTimerTime: number = pomodoroTime;
  let shortBreakTime: number = 10;
  let shortBreakTimerTime: number = shortBreakTime;
  let longBreakTime: number = 10;
  let longBreakTimerTime: number = longBreakTime;


  let comparisonNumber: number = 0;
  let toggleStart: number = 0;
  let canEdit: number = 0;
  let longStart: number = 1;
  let iteration: number = 1;



  function displayFormatter(z: number): string {
    if (z % 3600 / 60 < 10) {
      if (z % 60 > 9) {
        return "0" + Math.floor(z % 3600 / 60) + ":" + z % 60;
      } else {
        return "0" + Math.floor(z % 3600 / 60) + ":0" + z % 60;
      }
    } else {
      if (z % 60 > 9) {
        return Math.floor(z % 3600 / 60) + ":" + z % 60;
      } else {
        return Math.floor(z % 3600 / 60) + ":0" + z % 60;
      }
    }
  }

  function startTimer() {
    const startButton: HTMLElement | null = document.getElementById("start-button");
    if (startButton) {
      if (toggleStart === 0) {
        toggleStart = 1;
        canEdit = 1;
        startButton.innerText = "pause";
        timeInterval = setInterval(tickTimer , 100);
      } else {
        toggleStart = 0;
        clearInterval(timeInterval);
        startButton.innerText = "start";
      }
    }
  }

function tickTimer(){
  if (pomodoroTimerTime > 0) {
  currentPhase = "pomodoro " + iteration;
  mainDisplay = displayFormatter(pomodoroTimerTime);
  pomodoroTimerTime = pomodoroTimerTime - 1;
  console.log("pomodorotime");
  console.log(pomodoroTimerTime);
} else if (pomodoroTimerTime == 0 && shortBreakTimerTime > 0 && longStart % 4 != 0) {
  currentPhase = "short break " + iteration;
  mainDisplay = displayFormatter(shortBreakTimerTime);
  shortBreakTimerTime = shortBreakTimerTime - 1;
  console.log("shortbreaktime");
  console.log(shortBreakTimerTime);
} else if (pomodoroTimerTime == 0 && longBreakTimerTime > 0 && longStart % 4 == 0) {
  currentPhase = "long break " + Math.floor(iteration / 4);
  mainDisplay = displayFormatter(longBreakTimerTime);
  longBreakTimerTime = longBreakTimerTime - 1;
  console.log("longbreaktime");
  console.log(longBreakTimerTime);
}
else {
  console.log("nextiteration");
  pomodoroTimerTime = pomodoroTime;
  shortBreakTimerTime = shortBreakTime;
  longBreakTimerTime = longBreakTime;
  iteration++;
  longStart++;
}


}

  function resetTimer() {
    const startButton: HTMLElement | null = document.getElementById("start-button");
    if (startButton) {
      clearInterval(timeInterval);
      canEdit = 0;
      toggleStart = 0;
      longStart = 0;
      iteration = 1;
      startButton.innerText = "start";
      currentPhase = "pomodoro " + iteration;
      pomodoroTime = 1500;
      mainDisplay = pomodoroTime / 60 + ":00";
      pomodoroDisplay = pomodoroTime / 60 + ":00";
      shortBreakTime = 300;
      shortBreakDisplay = shortBreakTime / 60 + ":00";
      longBreakTime = 1500;
      longBreakDisplay = longBreakTime / 60 + ":00";
      pomodoroTimerTime = pomodoroTime;
      shortBreakTimerTime = shortBreakTime;
      longBreakTimerTime = longBreakTime;
    }
  }

  function adjustTime(type: string, operation: string) {
    switch (type) {
      case "pomodoro":
        if (canEdit === 0) {
          if (operation === "plus") {
            pomodoroTime += 60;
          } else if (operation === "minus") {
            pomodoroTime -= 60;
            if (pomodoroTime < 0) pomodoroTime = 0;
          }
          pomodoroTimerTime = pomodoroTime;
          pomodoroDisplay = pomodoroTime / 60 + ":00";
        }
        break;
      case "short-break":
        if (canEdit === 0) {
          if (operation === "plus") {
            shortBreakTime += 60;
          } else if (operation === "minus") {
            shortBreakTime -= 60;
            if (shortBreakTime < 0) shortBreakTime = 0;
          }
          shortBreakTimerTime = shortBreakTime;
          shortBreakDisplay = shortBreakTime / 60 + ":00";
        }
        break;
      case "long-break":
        if (canEdit === 0) {
          if (operation === "plus") {
            longBreakTime += 60;
          } else if (operation === "minus") {
            longBreakTime -= 60;
            if (longBreakTime < 0) longBreakTime = 0;
          }
          longBreakTimerTime = longBreakTime;
          longBreakDisplay = longBreakTime / 60 + ":00";
        }
        break;
    }
  }
</script>



<div id="black-outline">
  <div id="main-box">
    <p id="current-phase" class="box-name">{currentPhase}</p>
    <p id="main-display" class="big-time-display">{mainDisplay}</p>
  </div>
</div>

<div class="start-and-reset">
  <button id="start-button" class="left-button" on:click={startTimer}></button>
  <button id="reset-button" class="right-button" on:click={resetTimer}>reset</button>
</div>

<div class="settings">
  <div class="box">
    <p class="box-name">pomodoro</p>
    <p id="pomodoro-display" class="small-time-display">{pomodoroDisplay}</p>
    <button id="pomodoro-minus-button" class="minus-button" on:click={() => adjustTime('pomodoro', 'minus')}>-</button>
    <button id="pomodoro-plus-button" class="plus-button" on:click={() => adjustTime('pomodoro', 'plus')}>+</button>
  </div>

  <div class="box">
    <p class="box-name">short break</p>
    <p id="short-break-display" class="small-time-display">{shortBreakDisplay}</p>
    <button id="short-break-minus-button" class="minus-button" on:click={() => adjustTime('short-break', 'minus')}>-</button>
    <button id="short-break-plus-button" class="plus-button" on:click={() => adjustTime('short-break', 'plus')}>+</button>
  </div>

  <div class="box">
    <p class="box-name">long break</p>
    <p id="long-break-display" class="small-time-display">{longBreakDisplay}</p>
    <button id="long-break-minus-button" class="minus-button" on:click={() => adjustTime('long-break', 'minus')}>-</button>
    <button id="long-break-plus-button" class="plus-button" on:click={() => adjustTime('long-break', 'plus')}>+</button>
  </div>
</div>