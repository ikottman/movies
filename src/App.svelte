<script lang="ts">
  import EmojiSelector from 'svelte-emoji-selector';

  let movie = '';
  function onEmoji(event) {
    movie += event.detail;
  }

  let movies = [];

  function save() {
    movies = [...movies, movie];
    movie = '';
  }
</script>

<main>
  <ul>
    {#each movies as movie}
      <li>{movie}</li>
    {/each}
  </ul>
  <input bind:value={movie} type="text"/>
  <EmojiSelector on:emoji={onEmoji} />
  <button on:click={save}>💾</button>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }
</style>
