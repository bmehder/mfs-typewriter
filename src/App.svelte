<svelte:options tag="mfs-typewriter" />

<script>
  import { onMount } from "svelte";

  export let phrase = "Enter your phrase here...";
  export let delay = 0;
  export let speed = 100;
  export let url = "#";
  let index = 0;
  let typewriter;
  let typedChars = "";
  let finished;

  const typeChar = () => {
    if (index < phrase.length) {
      typedChars += phrase[index];
      index += 1;
    } else {
      clearInterval(typewriter);
      finished = true;
      index = 0;
    }
  };

  const start = (_delay = delay) => {
    setTimeout(() => typing(), _delay);
  };

  const typing = () => (typewriter = setInterval(typeChar, speed));

  const replay = (delay) => {
    typedChars = "";
    finished = false;
    start(delay);
  };

  onMount(() => start());
</script>

<section>
  <h3>
    <a class:finished href={url}>{@html typedChars}</a>
    {#if finished}
      <button on:click={() => replay(0)}>&#8634;</button>
    {/if}
  </h3>
</section>

<style>
  section {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-family: Arial, Helvetica, sans-serif;
  }
  h3 {
    position: relative;
    font-size: 3em;
    line-height: 3em;
    font-weight: 400;
    text-align: center;
    letter-spacing: 0.2em;
  }
  button {
    position: absolute;
    top: -0.75em;
    right: -0.5em;
    width: 2em;
    padding: 0.5em;
    font-size: 0.5em;
    line-height: 1em;
    border: 1px solid rgba(0, 0, 0, 0.24);
    border-radius: 50%;
    background: #fdc735;
    color: #333;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.24);
    cursor: pointer;
    transition: all 400ms;
  }
  button:hover {
    right: -1em;
    background-color: #307ad5;
    color: #fff;
    transition: all 400ms;
  }
  a {
    color: #307ad5;
    text-decoration: none;
    border: 0em solid #fdc735;
  }
  a:hover {
    padding: 0.5em 1em;
    border: 0.5em dotted #fdc735;
    transition: all 400ms ease-in-out;
  }
  .finished {
    padding: 0.5em;
    text-decoration: none;
    border-bottom: 0.5em solid #fdc735;
    transition: all 400ms ease-in-out;
  }
  @media screen and (max-width: 600px) {
    .hover {
      padding: initial;
    }
  }
</style>
