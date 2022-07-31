<script lang="ts">
  import EmojiSelector from 'svelte-emoji-selector';

  let movies = "ian test";
  
  function placeEmojiAtCursor(event) {
    const textArea = document.getElementById('movies');
    const emoji = event.detail;
    if (textArea.selectionStart || textArea.selectionStart == '0') {
        var startPos = textArea.selectionStart;
        var endPos = textArea.selectionEnd;
        textArea.value = textArea.value.substring(0, startPos)
            + emoji
            + textArea.value.substring(endPos, textArea.value.length);
    } else {
      textArea.value += emoji;
    }
  }

  function save() {
    const updatedMovies = document.getElementById('movies').value;
    console.log(updatedMovies);
  }
</script>

<main>
  <textarea id='movies' bind:value={movies} rows={movies.split('\n').length + 5}, cols=70/>
  <br/>
  <EmojiSelector on:emoji={placeEmojiAtCursor} />
  <br/>
  <button on:click={save}>💾</button>
</main>

<style>
  :root {
    font-family: 'Nunito Sans', sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  textarea {
    font-size: large;
  }
</style>
