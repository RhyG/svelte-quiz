<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { fly, fade } from "svelte/transition";

  import { CLOSE_EVENT } from "./constants";

  const dispatch = createEventDispatcher();
</script>

<div class="modal-bg" transition:fade>
  <div class="modal" transition:fly={{ y: -100 }}>
    <button
      on:click={() => {
        dispatch(CLOSE_EVENT);
      }}>Close</button
    >
    <!-- <slot>optional fallback</slot> -->
    <slot />
    <!-- <slot name="modal" /> -->
  </div>
</div>

<style>
  .modal-bg {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.8);
  }

  .modal {
    background: #fff;
    padding: 20px;
    border-radius: 15px;
  }
</style>
