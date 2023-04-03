<script>
    import Title from "./components/Title.svelte";
    import Timer from "./components/Timer.svelte";
    import Settings from "./components/Settings.svelte";
    
    let appName = "Pomo";
</script>

<!-- <Title title = {appName} /> -->
<!-- <h1><span class="accent-text">{appName}</span> - Pomodoro Timer</h1> -->
<div class="settings">
    <Settings />
</div>

<div class="timer">
    <Timer minutes={30} seconds={10}/>
</div>
