<!-- Timer -->
<script>
    export let minutes = 25;
    export let seconds = 0;
    let setTime = (minutes*60) + seconds; // Time in seconds
</script>

<div class="timer-container">
    <div class="progress-timer outer-circle">
        <div class="progress-timer inner-circle">
            <div class="time-count">
                {minutes}:{#if seconds < 10}0{seconds}{:else}{seconds}
                {/if}
            </div>
            
        </div>
    </div>
</div>