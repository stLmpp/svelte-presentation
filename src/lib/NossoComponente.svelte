<script lang="ts">
  import { countStore } from "./count.store";

  export let titulo: string;

  let oneWayDatabinding = "Texto one way";
  let twoWayDatabinding = "Text two way";

  let array = [1, 2, 3, 4, 5];

  let toggleVermelho = false;
  let styleColor = "blue";

  let parOuImpar = true;

  $: arrayFiltrado = array.filter((item) =>
    parOuImpar ? item % 2 === 0 : item % 2 !== 0
  );

  $: {
    console.log("parOuImpar", parOuImpar);
  }
</script>

<h2>{titulo}</h2>

<h3>Data binding</h3>

One way: {oneWayDatabinding}
<br />
<input value={oneWayDatabinding} />
<br />
Two way: {twoWayDatabinding}
<br />
<input bind:value={twoWayDatabinding} />

<h3>For each</h3>

<ul>
  {#each array as item, index}
    <li>{item} - {index}</li>
  {/each}
</ul>

<h3>If else</h3>

<ul>
  {#each array as item}
    {#if item % 2 === 0}
      <li>{item} - Par</li>
    {:else if item === 1}
      <li>É um</li>
    {:else}
      <li>{item} - Impar</li>
    {/if}
  {/each}
</ul>

<h3>Class</h3>

<div class:vermelho={toggleVermelho} class:fundo-preto={true}>
  Texto com diretiva class
</div>

<button on:click={() => (toggleVermelho = !toggleVermelho)}>
  Toggle vermelho
</button>

<h3>Style</h3>

<div style:color={styleColor} style:background-color="black">
  Diretiva style
</div>

<input bind:value={styleColor} />

<h3>Reatividade</h3>

<ul>
  {#each arrayFiltrado as item}
    <li>{item}</li>
  {/each}
</ul>

<label>
  <input type="checkbox" bind:checked={parOuImpar} />
  {parOuImpar ? "Par" : "Impar"}
</label>

<button on:click={() => (array = [...array, array.length + 1])}>
  Incrementar item no array
</button>

<h3>Stores (Componente filho)</h3>

Count store: {$countStore}

<button on:click={() => $countStore++}>Incrementar count store</button>

<style>
  .vermelho {
    color: red;
  }

  .fundo-preto {
    background-color: black;
  }
</style>
