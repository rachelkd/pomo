<script>
    import {blur, fade, fly} from 'svelte/transition';
    export let title = "Default title";
    export let timeModes = [{ phase: "work", minutes: 25, seconds: 0 }];
    export let toggleForm = () => {};
    export let changeTime = () => {};
    let phase;
    let minutes;
    let seconds;
    
    function handleClose() {
        toggleForm();
        // Change time functions need to be passed down into this comp from App.svelte
        for (let i in timeModes) {
            phase = timeModes[i].phase;
            console.log(phase);
            console.log("timemodes mins: " + timeModes[i].minutes);
            if(timeModes[i].minutes <= 59 && timeModes[i].minutes >= 0 && timeModes[i].seconds <= 59 && timeModes[i].seconds >= 0) {
                minutes = timeModes[i].minutes;
                console.log(minutes);
                seconds = timeModes[i].seconds;
                console.log(seconds);
                changeTime(phase, minutes, seconds);
            }
        }
        phase = null;
        minutes = null;
        seconds = null;   
    }
</script>

<div class="modal-container" in:blur out:fade>
    <div class="modal-content" transition:fly={{ y: 200 }}>
        <h2>{title}</h2>
        <button type = "button" class="close-btn" on:click={handleClose}><i class="fas fa-times" /></button>
        <p class="instructions">Change the minutes and seconds for the {title.toLowerCase()}</p>
        {#each timeModes as timeMode}
            <div class="input-container">
                <label for="minutes">Minutes: </label>
                <input type="number" id="minutes" min="0" max="59" bind:value={timeMode.minutes} />
                <label for="seconds">Seconds: </label>
                <input type="number" id="seconds" min="0" max="59" bind:value={timeMode.seconds} />
            </div>
        {/each}
    </div>
</div>