<!-- Timer -->
<script>
    import { onMount, onDestroy } from 'svelte';
    import { tick } from 'svelte';

    export let time = 0;
    export let timerStarted = false;
    export let handlePause = () => {};
    $: displayMinutes = Math.floor(time / 60);
    $: displaySeconds = time % 60; 
    let hovering = false;

    // Functions
    
    
</script>

<div class="timer-container">
    <div class="progress-timer outer-circle">
        <div class="progress-timer inner-circle">
            <div class="time-count">
                <button class = "timer-btn" on:click={ handlePause } >
                    <p>
                        {displayMinutes}:{displaySeconds < 10 ? '0' + displaySeconds : displaySeconds}
                    </p>
                </button>
            </div>
            
        </div>
    </div>
</div>