<script>
    import { setContext, getContext, onMount, onDestroy } from "svelte";
    import { tick } from 'svelte';
    import Title from "./components/Title.svelte";
    import Timer from "./components/Timer.svelte";
    import Settings from "./components/Settings.svelte";
    
    let appName = "Pomo";

    // Variables
    let minutes = 25;
    let seconds = 0;
    $: time = (minutes*60) + seconds; // Time in seconds
    let intervalId;
    let timerStarted = false;

    // Functions
    function startTimer() {
        timerStarted = true;
        intervalId = setInterval(() => {
            time--;
        }, 1000);
        
        console.log({timerStarted});
    }
    function stopTimer() {
        clearInterval(intervalId);
        timerStarted = false;
        console.log({timerStarted});
    }
    function handlePause() {
        if(timerStarted) {
            stopTimer();
        } else {
            startTimer();
        }
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
    {minutes}
    {seconds}
    {timerStarted} 
    {handlePause} />
</div>

<div class="timer">
    <Timer 
    {time} 
    {timerStarted} 
    {handlePause} />
</div>
