<script lang="ts">
    type Answer = "a" | "b" | "c" | "d";

    let result = "";
    let correctAnswer: Answer = "b";

    let answers: Answer[] = [ "a", "b", "c", "d" ]

    function pickAnswer(answer: Answer) {
        console.log('Picked', answer);
        if (answer === correctAnswer) {
            result = "Correct"!
            return;
        }

        result = "Wrong";
        return;
    }
</script>

<div>
    {#if result}
        <h4>{result}</h4>
    {:else}
        <h4>Choose an answer</h4>
    {/if}

    {#each answers as answer}
        <button on:click={() => pickAnswer(answer)}>Answer {answer.toUpperCase()}</button>
    {/each}
</div>