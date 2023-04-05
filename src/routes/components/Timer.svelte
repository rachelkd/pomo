<!-- Timer -->
<script>
    import { onMount, onDestroy } from 'svelte';
    import { fade } from 'svelte/transition';

    export let time = 0;
    export let currentPhase = "";
    export let handlePause = () => {};
    export let timerStarted = false;
    $: displayMinutes = Math.floor(time / 60);
    $: displaySeconds = time % 60; 
    let hovering = false;
    let statusText = "";
    let showStart = true;
    // Functions
    function handleHover() { // set statusText to the current phase name
        if(currentPhase === "work") {
            statusText = "work";
        } else if(currentPhase === "short-break") {
            statusText = "short break";
        } else {
            statusText = "long break";
        }
    }
    
</script>

<div class="timer-container">
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

    <div class="progress-circle">

    </div>
</div>