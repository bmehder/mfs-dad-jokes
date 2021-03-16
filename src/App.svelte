<svelte:options tag="mfs-dad-jokes" />

<script>
  import { onMount } from "svelte";

  let randomJoke;

  const getRandomJoke = async () => {
    const response = await fetch("https://icanhazdadjoke.com", {
      headers: { Accept: "application/json" },
    });
    const json = await response.json();

    return json.joke;
  };

  onMount(async () => {
    await onRandomJoke();
  });

  async function onRandomJoke() {
    try {
      randomJoke = await getRandomJoke();
    } catch (error) {
      console.log("Don't panic...but there was an error with the api request.");
    }
  }
</script>

<article>
  <h4>Random Dad Jokes</h4>
  <button on:click={onRandomJoke}>Get Another Joke</button>
  {#if randomJoke}
    <div>{randomJoke}</div>
  {:else}
    <p>Sorry, there was an error contacting the joke api. :-(</p>
  {/if}
</article>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  article {
    max-width: 400px;
    margin: auto;
    padding: 2em;
    display: flex;
    flex-direction: column;
    align-items: center;
    background: #307ad5;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 1em;
    color: #fff;
    border-radius: 16px;
  }
  h4 {
    margin: 1em 0;
    font-size: 1.2em;
    text-align: center;
    text-shadow: 0 0 2px rgba(0, 0, 0, 0.32);
  }
  button {
    width: 100%;
    padding: 1em;
    background: #fdc735;
    outline: none;
    border: none;
    border-radius: 4px;
    font-weight: bold;
    font-size: 1em;
    line-height: 1.5;
    color: #444;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.32);
    transition: all 400ms;
    text-transform: uppercase;
  }
  button:hover {
    background-image: linear-gradient(
      to bottom,
      transparent,
      rgba(0, 0, 0, 0.05)
    );
  }
  button:focus {
    outline: none;
  }
  p {
    line-height: 1.5;
  }
  div {
    margin: 1em 0;
    padding: 2em;
    background: #fff;
    color: #333;
    font-size: 18px;
    line-height: 1.5;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.32);
  }
</style>
