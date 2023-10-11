<script lang="ts">
  import { onMount } from "svelte";
  import { colors, moods } from "./App.svelte";
  import { scale } from "svelte/transition";
  import Chart from "./Chart.svelte";

  let container: HTMLElement;
  onMount(() => {
    container.scrollLeft = container.scrollWidth;
  });
</script>

<main bind:this={container}>
  {#each Object.entries($moods) as [date, mood]}
    <Chart {mood} {date} />
  {/each}
</main>

<style>
  main {
    width: 100%;
    height: 66%;
    overflow: auto;
    overflow-y: hidden;

    white-space: nowrap;
    padding: 20px;
  }
</style>
