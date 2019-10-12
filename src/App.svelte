<script>
  import { onMount } from 'svelte';

  const shrugs = [
    `¯\\_(ツ)_/¯`,
    `¯\\_( ͠° ͟ʖ °͠ )_/¯`,
    `乁( ⁰͡ Ĺ̯ ⁰͡ ) ㄏ`
  ];
	let activeShrug = shrugs[0];
  let input;

  onMount(() => {
    console.log('input ref:', input)
    input.select();
    document.execCommand('copy');
  });

  const copyShrug = (shrug) => {
    activeShrug = shrug
    input.select();
    document.execCommand('copy');
    console.log('Copied', shrug)
  }
</script>

<style>
	body {
    background-color: #223;
  }
  h1 {
		color: cornflowerblue;
	}
  input {
    /*visibility: hidden;*/
  }
</style>

<h1><code>{ activeShrug }</code></h1>

<p>☝️ has been copied to your clipboard</p>

<p>Here's some other shruggies:</p>

{#each shrugs as shrug}
<button on:click={() => copyShrug(shrug)}>
  <code>{shrug}</code>
</button>
{/each}


<input type="text" bind:this={input} value={activeShrug}>