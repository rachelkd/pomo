<script>
    import { setContext, getContext } from "svelte";
    import { fade } from 'svelte/transition';
    
    // Variables
    // export let minutes = 0;
    // export let seconds = 0;
    export let timerStarted = false;
    export let changePhase = () => {}; 

    export let handlePause = () => {};

    // Functions
    export let toggleWorkTimeForm = () => {};
    export let toggleBreakTimeForm = () => {};
</script>


<button class = btn on:click={ () => {
    toggleWorkTimeForm();
} }><i class="fa-regular fa-clock" /></button>
<button class = btn on:click={ () => {
    toggleBreakTimeForm();
} }><i class="fa-solid fa-mug-saucer" /></button>
<button class = btn on:click = { handlePause } >
    {#if !timerStarted} <!-- if timer paused -->
        <i class="fa-solid fa-play" />
        {:else}
        <i class="fa-solid fa-pause"></i>
    {/if}
</button>
<button class = btn on:click={ changePhase }><i class="fa-solid fa-forward-step" /></button>

