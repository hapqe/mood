<script lang="ts">
  import { draw, fade } from "svelte/transition";
  import { colors } from "./App.svelte";
  import { charts } from "./Toggle.svelte";
  export let index: number;
</script>

<!-- on:click={() => setMood(mood)} -->
{#if !$charts}
  <button>
    <svg width="43" height="43" viewBox="0 0 43 43">
      <path
        transition:fade
        d="M1.5 1.5H41.5V41.5H1.5V1.5Z"
        fill="#{colors[index]}"
        stroke-width="3"
      />
      <path
        transition:draw
        d="M1.5 1.5H41.5V41.5H1.5V1.5Z"
        fill="none"
        stroke="black"
        stroke-width="3"
      />
      <path
        transition:draw
        d="M8 18V18C14.0494 28.3064 28.9506 28.3064 35 18V18"
        fill="none"
        stroke="black"
        stroke-width="3"
      />
    </svg>
  </button>
{/if}
