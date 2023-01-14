<script lang="ts">
  export let question: any;

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
    isAnswered = true;
    isCorrect = correct;
  }
</script>

<h3>
  {@html question.question}
</h3>

{#if isAnswered}
  <h4>
    {#if isCorrect}
      Correct!
    {:else}
      Incorrect!
    {/if}
  </h4>
{/if}

{#each allAnswers as answer}
  <button on:click={() => checkQuestion(answer.correct)}>{@html answer.answer}</button>
{/each}

<style>
  button {
    margin-right: 10px;
  }
</style>
