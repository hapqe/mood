<script lang="ts">
  const hour = (new Date().getTime() / 1000 / 60 / 60).toFixed(0);

  let moods = JSON.parse(localStorage.getItem("moods") ?? "{}");
  let selectedMood = moods[hour];

  function setMood(mood: number) {
    console.log(moods);

    if (selectedMood === mood) {
      selectedMood = undefined;
      moods[hour] = undefined;
      localStorage.setItem("moods", JSON.stringify(moods));
      return;
    }

    selectedMood = moods[hour] = mood;
    localStorage.setItem("moods", JSON.stringify(moods));
  }
</script>

<main>
  <div class="wrapper">
    <h1 class="shadow">how do you feel?</h1>
    <div class="buttons">
      {#each Array(5).keys() as mood}
        <button on:click={() => setMood(mood)}>
          <img
            class="shadow {mood == selectedMood
              ? 'selected'
              : ''} {selectedMood !== undefined && mood !== selectedMood
              ? 'fade'
              : ''}"
            src="moods/{mood}.svg"
            alt="mood {mood}"
          />
        </button>
      {/each}
    </div>
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
    grid-template-rows: min-content 1fr;
    height: 100%;
  }

  .buttons {
    display: grid;
    gap: 20px;
  }

  .shadow {
    filter: drop-shadow(0 0 10px rgba(0, 0, 0, 0.2));
  }

  img {
    transition: 300ms;
  }

  /* button reset */
  button {
    border: none;
    background: none;
    padding: 0;
    cursor: pointer;
    -webkit-tap-highlight-color: transparent;
  }
</style>
