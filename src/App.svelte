<script context="module" lang="ts">
  import { writable } from "svelte/store";
  const m = JSON.parse(localStorage.getItem("moods") ?? "{}");

  export const hour = Math.floor(new Date().getTime() / 1000 / 60 / 60);

  export const moods = writable(m);
  export const selected = writable(m[hour]);
  export const colors = ["C6FFDD", "E3E9AD", "FBD786", "F9B182", "F7797D"];
</script>

<script lang="ts">
  import Toggle, { charts } from "./Toggle.svelte";
  import Charts from "./Charts.svelte";
  import Mood from "./Mood.svelte";

  function setMood(mood: number) {
    if ($selected === mood) {
      $selected = undefined;
      delete $moods[hour];
      localStorage.setItem("moods", JSON.stringify($moods));
      return;
    }

    $selected = $moods[hour] = mood;
    localStorage.setItem("moods", JSON.stringify($moods));
  }
</script>

<main>
  <div class="wrapper">
    <h1 class="shadow">how do you feel?</h1>
    {#if !$charts}
      <div class="buttons">
        {#each Array(5).keys() as mood}
          <Mood on:click={() => setMood(mood)} {mood} />
        {/each}
      </div>
    {:else}
      <Charts />
    {/if}
    <Toggle />
  </div>
</main>

<style>
  h1 {
    margin: 20px;
    color: black;
  }

  main {
    height: 100svh;
    width: 100svw;
    background-image: url("/dot.png");
    background-size: 16px;
    overflow: hidden;
  }

  .wrapper {
    display: grid;
    place-items: center;
    grid-template-rows: min-content 1fr min-content;
    height: 100%;
    padding-right: 20px;
    padding-left: 20px;
  }

  .buttons {
    display: grid;
    gap: 20px;
  }

  img {
    transition: 300ms;
  }
</style>
