<script lang="ts">
  import { draw, fade } from "svelte/transition";
  import { colors, selected } from "./App.svelte";
  import { charts } from "./Toggle.svelte";
  export let mood: number;
</script>

{#if !$charts}
  <button
    on:click
    class={$selected !== undefined
      ? $selected == mood
        ? "selected"
        : "fade"
      : ""}
  >
    <svg width="43" height="43" viewBox="0 0 43 43">
      <path
        in:fade|global
        d="M1.5 1.5H41.5V41.5H1.5V1.5Z"
        fill="#{colors[mood]}"
        stroke-width="3"
      />
      <path
        in:draw|global
        d="M1.5 1.5H41.5V41.5H1.5V1.5Z"
        fill="none"
        stroke="black"
        stroke-width="3"
      />
      <path
        in:draw|global
        d="M8 18V18C14.0494 28.3064 28.9506 28.3064 35 18V18"
        fill="none"
        stroke="black"
        stroke-width="3"
      />
    </svg>
  </button>
{/if}

<style>
  .selected {
    transform: scale(1.2);
    opacity: 1 !important;
  }

  * {
    transition: all 0.2s ease-in-out;
  }
</style>
