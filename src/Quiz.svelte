<script lang="ts">
  type Answer = "a" | "b" | "c" | "d";

  let result = "";
  let correctAnswer: Answer = "b";

  let answers: Answer[] = ["a", "b", "c", "d"];

  let quiz = getQuiz();

  function pickAnswer(answer: Answer) {
    if (answer === correctAnswer) {
      result = "Correct"!;
      return;
    }

    result = "Wrong";
    return;
  }

  async function getQuiz() {
    const res = await fetch("https://opentdb.com/api.php?amount=10&category=23&type=multiple");
    const quiz = await res.json();
    return quiz;
  }
</script>

<div>
  <button on:click={getQuiz}>Get quiz</button>
  {#if result}
    <h4 class={`${result === "Correct" ? "correct" : "incorrect"}`}>{result}</h4>
  {:else}
    <h4>Choose an answer</h4>
  {/if}

  {#each answers as answer}
    <button on:click={() => pickAnswer(answer)}>Answer {answer.toUpperCase()}</button>
  {/each}
</div>

<!-- https://opentdb.com/api.php?amount=10&category=23&type=multiple -->
<style>
  .correct {
    color: green;
  }

  .incorrect {
    color: red;
  }
</style>
