<script lang="ts">
  import Question from "./Question.svelte";

  let quiz = getQuiz();

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
  {#await quiz}
    <p>Loading...</p>
  {:then data}
    {#each data.results as question}
      <Question {question} />
    {/each}
  {/await}
</div>

<style>
</style>
