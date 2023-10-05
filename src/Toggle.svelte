<script context="module">
  import { writable } from "svelte/store";

  export const charts = writable(false);
</script>

<main>
  <button on:click={() => ($charts = !$charts)}>
    <svg
      class="shadow"
      transform="rotate({$charts ? 0 : -90})"
      width="50"
      height="50"
      viewBox="0 0 7 50"
    >
      {#each Array(5).keys() as i}
        <rect
          y={10 * i}
          x={$charts ? 0 : -20}
          width={$charts ? 7 : Math.random() * 50 + 5}
          height="7"
          fill="black"
        />
      {/each}
    </svg>
  </button>
</main>

<style>
  main {
    height: 100px;
    width: 100%;
    display: flex;
    justify-content: flex-end;
  }
  * {
    transition: 0.3s cubic-bezier(0.6, -0.28, 0.735, 0.045);
  }
</style>
