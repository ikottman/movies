<script lang="ts">
  import data from '@emoji-mart/data'
  import { init } from 'emoji-mart';

  init({ data })
  const movies = [{
    "title": "Pacific Rim",
    "giggle": "carrie",
    "emojis": "robot_face"
  }]
</script>

<main>
  <ul>
    {#each movies as movie}
      <li>{movie.title} | {movie.giggle} | <em-emoji id={movie.emojis} fallback={movie.emojis}/></li>
    {/each}
  </ul>
  
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
