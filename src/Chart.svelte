<script lang="ts">
  import { inview } from "svelte-inview";
  import { scale } from "svelte/transition";
  import { colors, hour } from "./App.svelte";

  export let mood: number;
  export let date: number;

  const d = new Date(date * 1000 * 60 * 60);
  const h = d.getHours() || 24;

  let info = "";

  if (hour == date) info = "Now";

  function random() {
    return Math.floor(Math.random() * 5);
  }

  let viewed = false;
</script>

<main
  use:inview
  on:inview_change={(e) => (viewed = e.detail.inView)}
  style="height: {90 / (5 / (5 - (mood ?? random())))}%; width: 2rem"
>
  {#if viewed}
    <div
      class="wrapper shadow {mood == null ? 'fade' : ''}"
      in:scale|global
      style="background: #{mood == null ? 'aaa' : colors[mood]};"
    >
      <div class="info">
        <h3
          style={mood == 4
            ? "transform: translate(-40%, -100%)"
            : "transform: translateX(-40%)"}
        >
          {info}
        </h3>
      </div>
    </div>
    <h4 in:scale|global class="shadow">{h}</h4>
  {/if}
</main>

<style>
  main {
    text-align: center;
    display: inline-block;
    margin-left: 10px;
    margin-right: 10px;
    min-height: fit-content;
  }
  .wrapper {
    outline: 3px solid black;
    width: 100%;
    height: 100%;
  }
  .info {
    position: absolute;
    writing-mode: vertical-rl;
    font-size: 10pt;
    bottom: 0;
  }
  h3 {
    margin-bottom: 10px;
    height: 100%;
  }
  span {
    font-size: 0.8rem;
    margin-top: 10px;
    margin-bottom: 10px;
    display: block;
  }
  h4 {
    margin: 0.3rem;
  }
</style>
