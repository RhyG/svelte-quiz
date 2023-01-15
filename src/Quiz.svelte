<script lang="ts">
  import { onMount, beforeUpdate, afterUpdate, onDestroy } from "svelte";
  import { fly } from "svelte/transition";

  import { score } from "./store";

  import Modal from "./Modal.svelte";
  import Question from "./Question.svelte";

  let activeQuestion = 0;

  let quiz = getQuiz();

  let isModalOpen = false;

  onMount(() => {
    console.log("I mounted");
  });

  beforeUpdate(() => {
    console.log("I am about to update");
  });

  afterUpdate(() => {
    console.log("I updated");
  });

  onDestroy(() => {
    console.log("I destroyed");
  });

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
    score.set(0);

    quiz = getQuiz();
    isModalOpen = false;
  }

  // Reactive expression
  $: if ($score > 0) {
    isModalOpen = true;
  }

  // Reactive declaration
  $: questionNumber = activeQuestion + 1;
</script>

<div>
  <button on:click={resetQuiz}>Start new quiz</button>

  <h3>My Score: {$score}</h3>
  <h4>Question #{questionNumber}</h4>

  {#await quiz}
    <p>Loading...</p>
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <div in:fly={{ x: 100 }} out:fly={{ x: -200 }} class="fade-wrapper">
          <Question {question} {nextQuestion} />
        </div>
      {/if}
    {/each}
  {/await}
</div>

{#if isModalOpen}
  <Modal on:CLOSE_EVENT={resetQuiz}>
    <h2>You won!</h2>
    <p>Congratulations</p>
    <button on:click={resetQuiz}>Start over</button>
  </Modal>
{/if}

<style>
  .fade-wrapper {
    position: absolute;
  }
</style>
