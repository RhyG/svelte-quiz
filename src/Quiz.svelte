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

  function handleClick() {
    quiz = getQuiz();
  }
</script>

<div>
  <button on:click={handleClick}>Get quiz</button>
  {#if result}
    <h4 class={`${result === "Correct" ? "correct" : "incorrect"}`}>{result}</h4>
  {:else}
    <h4>Choose an answer</h4>
  {/if}

  {#await quiz}
    <p>Loading...</p>
  {:then data}
    <h3>{data.results[0].question}</h3>
  {/await}

  {#each answers as answer}
    <button on:click={() => pickAnswer(answer)}>Answer {answer.toUpperCase()}</button>
  {/each}
</div>

<style>
  .correct {
    color: green;
  }

  .incorrect {
    color: red;
  }
</style>
