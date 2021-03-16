<svelte:options tag="mfs-dad-jokes" />

<script>
  import { onMount } from "svelte";

  let joke;

  const getRandomJoke = async () => {
    const response = await fetch("https://icanhazdadjo1ke.com", {
      headers: { Accept: "application/json" },
    });
    const json = await response.json();

    return json.joke;
  };

  onMount(async () => {
    await onRandomJoke();
  });

  const onRandomJoke = async () => {
    try {
      joke = await getRandomJoke();
    } catch (error) {
      console.log(error);
    }
  };
</script>

<article>
  <h4>Random Dad Jokes</h4>
  <button on:click={onRandomJoke}>Get Another Joke</button>
  {#if joke}
    <div>{joke}</div>
  {:else}
    <div>A new joke is loading...</div>
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
    box-shadow: none;
  }
  button:focus {
    outline: none;
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
