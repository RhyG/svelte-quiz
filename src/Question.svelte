<script lang="ts">
  import { score } from "./store";

  export let question: any;
  export let nextQuestion: () => void;

  let isCorrect: boolean;
  let isAnswered = false;

  let answers = question.incorrect_answers.map((answer) => {
    return {
      answer,
      correct: false,
    };
  });

  let allAnswers = [...answers, { answer: question.correct_answer, correct: true }];

  shuffle(allAnswers);

  function shuffle(array: any[]) {
    return array.sort(() => Math.random() - 0.5);
  }

  function checkQuestion(correct: boolean) {
    if (!isAnswered) {
      isAnswered = true;
      isCorrect = correct;

      if (correct) {
        score.update((value) => value + 1);
      }
    }
  }
</script>

<h3>
  {@html question.question}
</h3>

{#if isAnswered}
  <h5 class:correct={isCorrect} class:wrong={!isCorrect}>
    {#if isCorrect}
      Correct!
    {:else}
      Incorrect!
    {/if}
  </h5>
{/if}

{#each allAnswers as answer}
  <button on:click={() => checkQuestion(answer.correct)}>{@html answer.answer}</button>
{/each}

{#if isAnswered}
  <div><button on:click={nextQuestion}>Next question</button></div>
{/if}

<style>
  button {
    margin-right: 10px;
  }

  h5.wrong {
    color: red;
  }

  h5.correct {
    color: green;
  }
</style>
