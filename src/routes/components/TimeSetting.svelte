<script>
    import {blur, fade, fly} from 'svelte/transition';
    export let timeModes = ["work"];
    export let toggleForm = () => {};
    export let minutes = 25;
    export let seconds = 0;
    
</script>

<div class="modal-container" in:blur out:fade>
    <div class="modal-content" transition:fly={{ y: 200 }}>
        <h3>Timer Settings</h3>
        <button type = "button" class="close-btn" on:click={toggleForm}><i class="fas fa-times" /></button>
    </div>
</div>