<script lang="ts">
  import { inview } from "svelte-inview";
  import { fade, fly, scale, slide } from "svelte/transition";
  import { colors } from "./App.svelte";

  export let mood: number;
  export let date: number;

  const hour = date % 24;
  let viewed = false;
</script>

<main
  use:inview
  on:inview_change={(e) => (viewed = e.detail.inView)}
  style="height: {90 / (5 / (5 - mood))}%; width: 2rem"
>
  {#if viewed}
    <div
      class="wrapper shadow"
      in:scale|global
      style="background: #{colors[mood]};"
    >
      <div class="info">
        <h3
          style={mood == 4
            ? "transform: translate(-40%, -100%)"
            : "transform: translateX(-40%)"}
        >
          Yesterday
        </h3>
      </div>
    </div>
    <h4 in:scale|global={{ axis: "x" }} class="shadow">{hour}</h4>
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
