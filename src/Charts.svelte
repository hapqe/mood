<script>
  import { onMount } from "svelte";
  import { colors, moods } from "./App.svelte";
  import { scale } from "svelte/transition";
  import Chart from "./Chart.svelte";

  let container;
  onMount(() => {
    container.scrollLeft = container.scrollWidth;
  });

  function fill(obj) {
    const keys = Object.keys(obj);
    const first = keys[0];
    const last = keys[keys.length - 1];

    const ret = {};

    for (let i = first; i <= last; i++) {
      ret[i] = obj[i] ?? null;
    }

    return ret;
  }
</script>

<main bind:this={container}>
  {#each Object.entries(fill($moods)) as [date, mood]}
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
