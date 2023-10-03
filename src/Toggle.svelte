<script lang="ts">
    import { writable } from "svelte/store";

    const ys = [0, 10, 20, 30, 40];

    const charts = writable(false);
</script>

<button on:click={() => ($charts = !$charts)}>
    <svg
        transform="rotate({$charts ? 0 : -90})"
        width="50"
        height="50"
        viewBox="0 0 7 50"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
    >
        {#each Array(5).keys() as i}
            <rect
                y={ys[i]}
                x={$charts ? 0 : -20}
                width={$charts ? 7 : Math.random() * 50 + 5}
                height="7"
                fill="black"
            />
        {/each}
    </svg>
</button>

<style>
    svg {
        margin: 20px;
    }
    * {
        transition: 0.3s cubic-bezier(0.6, -0.28, 0.735, 0.045);
    }
</style>
