<script lang="ts">
  import { fly } from "svelte/transition";
  import Question from "./Question.svelte";

  let activeQuestion = 0;
  let score = 0;

  let quiz = getQuiz();

  async function getQuiz() {
    const res = await fetch("https://opentdb.com/api.php?amount=10&category=23&type=multiple");
    const quiz = await res.json();
    return quiz;
  }

  function nextQuestion() {
    activeQuestion += 1;
  }

  function resetQuiz() {
    activeQuestion = 0;
    score = 0;

    quiz = getQuiz();
  }

  function addToScore() {
    score = score + 1;
  }
</script>

<div>
  <button on:click={resetQuiz}>Start new quiz</button>

  <h3>My Score: {score}</h3>
  <h4>Question #{activeQuestion + 1}</h4>

  {#await quiz}
    <p>Loading...</p>
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <div in:fly={{ x: 100 }} out:fly={{ x: -200 }} class="fade-wrapper">
          <Question {question} {nextQuestion} {addToScore} />
        </div>
      {/if}
    {/each}
  {/await}
</div>

<style>
  .fade-wrapper {
    position: absolute;
  }
</style>
