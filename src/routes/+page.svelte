<script>
    import Title from "./components/Title.svelte";
    import Timer from "./components/Timer.svelte";
    
    let appName = "Pomo";
</script>

<!-- <Title title = {appName} /> -->
<!-- <h1><span class="accent-text">{appName}</span> - Pomodoro Timer</h1> -->
<div class="timer">
    <Timer />
</div>
