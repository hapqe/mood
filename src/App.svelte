<script context="module" lang="ts">
  import { writable } from "svelte/store";

  export const moods = writable(
    JSON.parse(localStorage.getItem("moods") ?? "{}")
  );
  export const colors = ["C6FFDD", "E3E9AD", "FBD786", "F9B182", "F7797D"];
</script>

<script lang="ts">
  $moods = {
    471223: 0,
    471224: 0,
    471225: 2,
    471226: 0,
    471227: 0,
    471228: 0,
    471229: 0,
    471230: 3,
    471231: 2,
    471232: 1,
    471233: 4,
    471234: 0,
  };
  import Toggle, { charts } from "./Toggle.svelte";
  import Charts from "./Charts.svelte";
  import Mood from "./Mood.svelte";

  const hour = Math.floor(new Date().getTime() / 1000 / 60 / 60);

  let selectedMood = $moods[hour];

  function setMood(mood: number) {
    if (selectedMood === mood) {
      selectedMood = undefined;
      $moods[hour] = undefined;
      localStorage.setItem("moods", JSON.stringify($moods));
      return;
    }

    selectedMood = $moods[hour] = mood;
    localStorage.setItem("moods", JSON.stringify($moods));
  }
</script>

<main>
  <div class="wrapper">
    <h1 class="shadow">how do you feel?</h1>
    {#if !$charts || true}
      <div class="buttons">
        {#each Array(5).keys() as mood}
          <Mood index={mood} />
          <!-- <button on:click={() => setMood(mood)}> -->
          <!--   <img -->
          <!--     class="shadow {mood == selectedMood -->
          <!--       ? 'selected' -->
          <!--       : ''} {selectedMood !== undefined && mood !== selectedMood -->
          <!--       ? 'fade' -->
          <!--       : ''}" -->
          <!--     src="moods/{mood}.svg" -->
          <!--     alt="mood {mood}" -->
          <!--   /> -->
          <!-- </button> -->
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

  .fade {
    opacity: 0.5;
    filter: grayscale(1) !important;
  }

  .selected {
    transform: scale(1.2);
    opacity: 1 !important;
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
