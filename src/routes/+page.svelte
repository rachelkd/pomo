<script>
    import { setContext, getContext, onMount, onDestroy } from "svelte";
    // import Title from "./components/Title.svelte";
    import Timer from "./components/Timer.svelte";
    import Settings from "./components/Settings.svelte";
    import TimeSetting from "./components/TimeSetting.svelte";

    import timeDefaults from "./times.js";
    
    let appName = "Pomo";

    // Variables
    let times = [...timeDefaults];
    let phaseCycle = ["work", "short-break", "work", "long-break"];
    let phaseCycleIndex = 0;
    let current = { phase: "work", minutes: 25, seconds: 0 };
    $: minutes = current.minutes;
    $: seconds = current.seconds;
    // Testing seconds:
    // let minutes = 0;
    // let seconds = 3;
    $: time = (minutes*60) + seconds; // Time in seconds
    let intervalId;
    let timerStarted = false;
    // Alarm:
    let alarm;
    // Time settings
    let showTimeSettings = false;
    let showBreakSettings = false;
    let workSettings = times.filter(obj => obj.phase === "work");
    let breakSettings = times.filter(obj => obj.phase === "short-break" || obj.phase === "long-break");
    let setPhase = null;

    // Functions
    function startTimer() {
        timerStarted = true;
        intervalId = setInterval(() => {
            time--;
            if(time === 0) { // Stop timer when it hits 0 seconds
                stopTimer();
                alarm.play(); // Play alarm sound
            }
        }, 1000);
        
        console.log({timerStarted});
    }
    function stopTimer() {
        clearInterval(intervalId);
        timerStarted = false;
        console.log({timerStarted});
    }
    function handlePause() {
        if(!timerStarted && time != 0) {
            startTimer();
        } else {
            stopTimer();
        }
    }
    function changePhase() {
        stopTimer();
        if(phaseCycleIndex < 3) {
            phaseCycleIndex++;
        } else {
            phaseCycleIndex = 0;
        }
        current = times.find(item => item.phase === phaseCycle[phaseCycleIndex]);
        console.log("Phase changed: ");
        console.log({current});
    }
    function toggleWorkTimeForm() {
        showTimeSettings = !showTimeSettings;
        showBreakSettings = false;
        console.log({showTimeSettings});
        console.log({showBreakSettings});
    }
    function toggleBreakTimeForm() {
        showBreakSettings = !showBreakSettings;
        showTimeSettings = false;
        console.log({showBreakSettings});
        console.log({showTimeSettings});
    }
    // Time Settings functions
    function changeTime(phase, minutes, seconds) {
        setPhase = times.find(item => item.phase === phase);
        if(setPhase) {
            setPhase.minutes = minutes;
            setPhase.seconds = seconds;
            console.log(`Changed time for ${setPhase.phase} to ${setPhase.minutes} minutes and ${setPhase.seconds} seconds`);
        }
        setPhase = null;
        current = times.find(item => item.phase === phaseCycle[phaseCycleIndex]);
    }

    // Lifecycle functions
    onDestroy(() => {
        stopTimer();
    });
</script>

<!-- <Title title = {appName} /> -->
<!-- <h1><span class="accent-text">{appName}</span> - Pomodoro Timer</h1> -->
<div class="settings">
    <Settings
    {timerStarted} 
    {changePhase}
    {handlePause}
    {toggleWorkTimeForm}
    {toggleBreakTimeForm} />
</div>

<div class="timer">
    <Timer 
    {time} 
    {timerStarted} 
    {handlePause} 
    {current} />
</div>

<div class="timer-settings">
    {#if showTimeSettings}
        <TimeSetting
        title = {"Work Time"}
        timeModes={workSettings}
        toggleForm={toggleWorkTimeForm}
        {changeTime} />
    {/if}
    {#if showBreakSettings}
        <TimeSetting
        title = {"Break Times"}
        timeModes={breakSettings}
        toggleForm={toggleBreakTimeForm}
        {changeTime} />
    {/if}
</div>


<audio src="https://github.com/rachelkd/pomo/blob/main/static/audio/timer_done.mp3?raw=true" bind:this={alarm}></audio>