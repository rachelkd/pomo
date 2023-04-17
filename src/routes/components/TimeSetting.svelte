<script>
    import {blur, fade, fly} from 'svelte/transition';
    export let timeModes = ["work"];
    export let toggleForm = () => {};
    
</script>

<div class="modal-container" in:blur out:fade>
    <div class="modal-content" transition:fly={{ y: 200 }}>
        <p>{timeModes}</p>
        <button type = "button" class="close-btn" on:click={toggleForm}><i class="fas fa-times" /></button>
    </div>
</div>