<script>
    import { setContext, getContext } from "svelte";
    import { fade } from 'svelte/transition';
    
    // Variables
    export let minutes = 0;
    export let seconds = 0;
    export let timerStarted = false;
    export let changePhase = () => {}; 

    // export let startTimer = () => {};
    // export let stopTimer = () => {};
    export let handlePause = () => {};

    let showTimeSettings = false;
    let showBreakSettings = false;

    // Functions
    
</script>


<button class = btn on:click={ () => {
    showTimeSettings = !showTimeSettings;
    showBreakSettings = false;
    // console.log({showTimeSettings});
} }><i class="fa-regular fa-clock" /></button>
<button class = btn on:click={ () => {
    showBreakSettings = !showBreakSettings;
    showTimeSettings = false;
    // console.log({showBreakSettings});
} }><i class="fa-solid fa-mug-saucer" /></button>
<button class = btn on:click = { handlePause } >
    {#if !timerStarted} <!-- if timer paused -->
        <i class="fa-solid fa-play" />
        {:else}
        <i class="fa-solid fa-pause"></i>
    {/if}
</button>
<button class = btn on:click={ changePhase }><i class="fa-solid fa-forward-step" /></button>

