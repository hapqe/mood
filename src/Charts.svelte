<script lang="ts">
  import { onMount } from "svelte";
  import { colors, moods } from "./App.svelte";
  console.log(Object.values($moods));

  let container: HTMLElement;
  onMount(() => {
    container.scrollLeft = container.scrollWidth;
  });
</script>

<main bind:this={container}>
  {#each Object.values($moods) as mood}
    <div
      class="shadow"
      style="background: #{colors[mood]}; height: {100 /
        (5 / (5 - mood))}%; width: 2rem"
    />
  {/each}
</main>

<style>
  main {
    width: 100%;
    height: 100%;
    overflow: auto;
    overflow-y: hidden;

    white-space: nowrap;
    padding: 20px;
  }
  div {
    display: inline-block;
    margin-left: 10px;
    margin-right: 10px;
    outline: 3px solid black;
  }
</style>
