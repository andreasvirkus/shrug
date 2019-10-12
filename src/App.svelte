<script>
  import { onMount } from 'svelte';

  const shrugs = [
    `¯\\_(ツ)_/¯`,
    `¯\\_( ͠° ͟ʖ °͠ )_/¯`,
    `乁( ⁰͡ Ĺ̯ ⁰͡ ) ㄏ`
  ];
	let activeShrug = shrugs[0];
  let input;
  let copied = false;

  const copyShrug = (shrug) => {
    if (shrug) activeShrug = shrug;

    input.select();
    document.execCommand('copy');
    console.log('Copied', shrug);
    copied = true
  };

  const handleKeydown = (event) => {
    console.log('Key pressed', event)
    if (event.code === 'Space') {
      copyShrug();
    }
  };
</script>

<style>
	:global(body) {
    background-color: #223;
    color: beige;
    font-family: 'SFMono-Regular', Menlo, Consolas, 'Liberation Mono', Courier, monospace;;
  }
  main {
    width: 95%;
    max-width: 45rem;
    margin: 2rem auto;
  }
  h1 {
		color: cornflowerblue;
    text-align: center;
    margin-bottom: 2rem;
	}
  h2 {
    text-align: center;
  }
  input {
    opacity: 0;
    pointer-events: none;
  }
  button {
    background: none;
    border: none;
    padding: .5rem 1rem;
    color: beige;
    cursor: pointer;
    border-radius: 4px;
    margin: 0;
  }
  button:hover {
    background-color: rgba(255, 255, 255, 0.2);
  }
  fieldset {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: none;
    background-color: rgba(255, 255, 255, 0.2);
    padding: 1.5rem 1rem;
    border-radius: 4px;
  }
</style>

<svelte:window on:keydown={handleKeydown}/>

<main>
  <h1><code>{ shrugs[0] }</code></h1>

  <p><strong>Here's the thing.</strong> Sometimes I'll need this ☝️ expressive set of characters
  in a way that Slack's <code>/shrug</code> command doesn't allow me to.
  For example, to prepend it to a sentence or use it in the middle of a text.
  Maybe I'll use it somewhere other than Slack. Anywho, this website
  was created so I'd always have a quick way to copy it or other similar shruggies.</p>

  {#if !copied}
  <h2>Hit <code>Space</code> to copy the default shrug or click on another one</h2>
  {:else}
  <h2>Copied: <code>{ activeShrug }</code></h2>
  {/if}

  <p>Meet our shruggies!</p>

  <fieldset>
  {#each shrugs as shrug}
    <button on:click={() => copyShrug(shrug)} type="button">
      <code>{shrug}</code>
    </button>
  {/each}
  </fieldset>


  <input type="text" bind:this={input} value={activeShrug}>
</main>