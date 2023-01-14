<script>
    export let quizName = "Rhys Quiz";
    let presses = 0;

    // let title = ""
    let a = 0;
    let b = 0;

    function onClick() {
        presses += 1
    }
</script>

<div>
    <h2>{quizName}</h2>
    <!-- <h4>{title}</h4>
    <input bind:value={title} type="text"> -->
    
    <input type="number" bind:value={a}>
    <input type="number" bind:value={b}>
    <h4>{a + b}</h4>
    <button on:click={onClick}>Press me</button>
    <p>Number of presses: {presses}</p>
</div>