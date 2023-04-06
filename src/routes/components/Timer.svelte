<!-- Timer -->
<script>
    import { onMount, onDestroy } from 'svelte';
    import { fade } from 'svelte/transition';
    import { tweened } from 'svelte/motion';

    export let time = 0;
    export let current = {phase: "work", minutes: 25, seconds: 0};
    export let handlePause = () => {};
    export let timerStarted = false;
    $: displayMinutes = Math.floor(time / 60);
    $: displaySeconds = time % 60; 
    $: totalSeconds = (current.minutes*60) + current.seconds;
    // Testing:
    // let totalSeconds = 3;
    $: timeCompleted = (totalSeconds - time)/totalSeconds; // Decimal number of time elapsed over total time
    $: strokeDashOffset = 1068 * (1-timeCompleted);
    let hovering = false;
    let statusText = "";
    let showStart = true;
    // Functions
    function handleHover() { // set statusText to the current phase name
        if(current.phase === "work") {
            statusText = "work";
        } else if(current.phase === "short-break") {
            statusText = "short break";
        } else {
            statusText = "long break";
        }
    }
    
</script>
<style>
    circle {
	fill: none;
	stroke: var(--color-theme-1);
	stroke-width: 20px;
	transform: rotate(-90deg);
	stroke-dasharray: 1068;
	stroke-dashoffset: var(--strokeDashOffset); /* Start at 1068 then count down as time proceeds to 0*/
    }
    svg {
        position: absolute;
        top: 0px;
        left: 0px;
    }
</style>

<div class="timer-container">
    <div class="progress-circle"
        style = "
        --strokeDashOffset: {strokeDashOffset};
        ">
        <svg xmlns="http://www.w3.org/2000/svg" version="2" width="360px" height="360px">
            <circle cx="-180" cy="180" r="170" stroke-linecap="round" />        
        </svg>
    </div>
    <div class="progress-timer outer-circle">
        <div class="progress-timer inner-circle">  
            <div class="time-count">
                <button class = "timer-btn" on:click={ () => {
                    handlePause();
                    showStart = false;
                    } } 
                    on:mouseover = { () => {
                    hovering = true;
                    handleHover();
                    } } on:focus = { () => {} } on:mouseleave = { () => {hovering = false;} }>
                    <p>
                        {#if hovering && !timerStarted && showStart}
                            <p class="hover" in:fade>
                                press to<br>start
                            </p>
                        {:else if hovering && !timerStarted}
                            <p class="hover" in:fade>
                                {statusText}
                            </p>
                        {:else}
                            <p in:fade>{displayMinutes}:{displaySeconds < 10 ? '0' + displaySeconds : displaySeconds}</p>
                        {/if}
                    </p>
                </button>
            </div>          
        </div>
    </div>
</div>