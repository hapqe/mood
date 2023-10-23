<script lang="ts">
  import { draw, fade } from "svelte/transition";
  import { colors, mood } from "./App.svelte";
  import { charts } from "./Toggle.svelte";
</script>

<div class="buttons">
  {#each Array(5).keys() as m}
    <button
      on:click={() => {
        $mood = m;
      }}
    >
      <svg width="43" height="43" viewBox="0 0 43 43">
        <path
          in:fade|global
          d="M1.5 1.5H41.5V41.5H1.5V1.5Z"
          fill="#{colors[m]}"
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
  {/each}
</div>

<style>
  .buttons {
    display: grid;
    gap: 20px;
  }
</style>
