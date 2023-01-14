<script lang="ts">
    type Answer = "a" | "b" | "c" | "d";

    let result = "";
    let correctAnswer: Answer = "b";

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
    <h4>{result}</h4>
    <button on:click={() => pickAnswer("a")}>Answer A</button>
    <button on:click={() => pickAnswer("b")}>Answer B</button>
    <button on:click={() => pickAnswer("c")}>Answer C</button>
    <button on:click={() => pickAnswer("d")}>Answer D</button>
</div>