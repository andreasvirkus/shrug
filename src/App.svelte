<script>
  import { tick } from 'svelte';

  const shrugs = [
    `¯\\_(ツ)_/¯`,
    `¯\\_( ͠° ͟ʖ °͠ )_/¯`,
    `乁( ⁰͡ Ĺ̯ ⁰͡ ) ㄏ`
  ];
	let activeShrug = shrugs[0];
  let input;
  let copied = false;

  const copyShrug = async (shrug) => {
    console.log('shrug to copy:', shrug || activeShrug)
    if (shrug) activeShrug = shrug;
    console.log({ activeShrug })

    await tick();
    input.select();
    document.execCommand('copy');
    console.log('Copied', activeShrug);
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
    font-family: 'SFMono-Regular', Menlo, Consolas, 'Liberation Mono', Courier, monospace;
  }
  main {
    width: 95%;
    max-width: 45rem;
    margin: 2rem auto;
  }
  main > * {
    margin-bottom: 3rem;
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
    position: fixed;
    top: -10vh;
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
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    border: none;
    border: 1px solid;
    padding: 1.5rem 1rem;
    border-radius: 4px;
  }
  .emoji {
    font-family: initial;
  }
  .key {
    font-size: 2.25rem;
    padding: .2rem .5rem;
    border-radius: .25rem;
    background-color: rgba(255, 255, 255, 0.2);
  }
  footer {
    text-align: center;
  }
  a {
    color: white;
  }
</style>

<svelte:window on:keydown={handleKeydown}/>

<main>
  <h1><code>{ shrugs[0] }</code></h1>

  <p><strong>Here's the thing.</strong> Sometimes I'll need this
    <span class="emoji">☝️</span> expressive set of characters
  in a way that Slack's <code>/shrug</code> command doesn't allow me to.
  For example, to prepend it to a sentence or use it in the middle of a text.
  Maybe I'll use it somewhere other than Slack. Anywho, this website
  was created so I'd always have a quick way to copy it or other similar shruggies.</p>

  {#if !copied}
  <h2>hit <code class="key">Space</code> to copy the default shrug or click on another one</h2>
  {:else}
  <h2>Copied: <code>{ activeShrug }</code></h2>
  {/if}


  <fieldset>
    <legend>Meet our shruggies!</legend>
    {#each shrugs as shrug}
    <button on:click={() => copyShrug(shrug)} type="button">
      <code>{shrug}</code>
    </button>
    {/each}
  </fieldset>


  <input type="text" bind:this={input} value={activeShrug}>

  <footer>
    <a href="https://github.com/andreasvirkus/shrug">Source</a>
   | <a href="https://andreasvirkus.me?utm_source=shrug.andreasvirkus.me" target="_blank" rel="noopener noreferrer">Author</a>
  </footer>

  <a href="https://github.com/andreasvirkus/shrug" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#fff; color:#223; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>
</main>
