<script>
  import svelteLogo from './assets/svelte.svg'
  import Child from './lib/Child.svelte'

  let name = "Markus";
  let age = 35;
  let warning = null;
  let mytodos = [{"desc": "Einkaufen", "done": false}, {"desc": "Kochen", "done": false}, {"desc": "Programmieren", "done": true}]
  $: upper = name.toUpperCase()

  $: if (age > 40) {
    warning = "Zu alt";
  } else {
    warning = "Alles im grünen Bereich"
  }

  const increaseAge = () => {
    age += 1;
  }

  const decreaseAge = () => {
    age -= 1;
  }


</script>

<main>
  <h3>Vite + Svelte</h3>
  <p>{name}</p>
  <p>{age}</p>
  <p>{upper}</p>
  <p class="{age > 40 ? "warning": "ok"}">{warning}</p>
  <button on:click={increaseAge}>Increase Age</button>
  <button on:click|once|preventDefault={decreaseAge}>Decrease Age</button>
  <!-- <input type="text" value="{name}"> -->
  <input type="text" bind:value={name}>
  {#if age > 40}
  <p>Du bist zu alt</p>
  {:else}
  <p>Du bist nicht zu alt</p>
  {/if}
  <!-- <p>{mytodos[0]}</p> -->
  {#each mytodos as item, index}
     <p class={item.done ? "ok" : "warning"}>Todo nummer: {index + 1} {item.desc}</p>
  {:else}
    <p>Noch keine Todos!</p>
  {/each}

  <hr/>
  <Child/>

</main>

<style>
  .warning {
    color: white;
    background-color: darkred;
  }

  .ok {
    color: white;
    background-color: darkgreen;
  }
</style>
