<script lang="ts">
  import { createPopup } from '@picmo/popup-picker';
  import { onMount } from 'svelte';

  let movies = "ian test";
  let picker;
  // TODO: pull out emoji picker to a separate component, will need to pass down the text area element
  onMount(async() => {
    const triggerButton = document.getElementById('emoji') as HTMLElement;
    picker = createPopup({
      showVariants: false,
    }, {
      triggerElement: triggerButton,
      referenceElement: triggerButton,
      position: 'bottom-start'
    });
    picker.addEventListener('emoji:select', placeEmojiAtCursor);
  });
  
  function placeEmojiAtCursor(event) {
    const textArea = document.getElementById('movies');
    const emoji = event.emoji;
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
  <textarea id='movies' bind:value={movies} rows={movies.split('\n').length + 5}, cols=90/>
  <br/>
  <button id='emoji' on:click={() => picker.toggle()}>Emoji</button>
  <button on:click={save}>Save</button>
</main>

<style>
  :root {
    font-family: 'Nunito Sans', sans-serif;
    background-color: #1d1d1d;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  textarea {
    color: #fff;
    font-size: large;
    white-space: nowrap;
    background-color: #353b45;
    border: 2px transparent;
    padding: 5px;
  }

  textarea:focus {
    /* border: 2px solid #264437; */
    box-shadow: 0 0 10px #42b983;
  }

  button {
    color: #fff;
    background-color: #5865f2;
    align-items: center;
    justify-content: center;
    min-height: 32px;
    min-width: 100px;
    margin: 4px 8px 4px 0;
    padding: 2px 16px;
    border: 0;
    border-radius: 3px;
    box-sizing: border-box;
    cursor: pointer;
    transition: background-color .3s ease,color .3s ease;
  }

  button:hover {
    background-color: #4752c4;
  }
</style>
