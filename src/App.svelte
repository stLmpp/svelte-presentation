<script lang="ts">
  import { countStore } from "./lib/count.store";
  import NossoComponente from "./lib/NossoComponente.svelte";

  let count = 0;

  let titulo = "Nosso componente Teste";
</script>

<h1>Introdução ao Svelte</h1>

<button on:click={() => count++}>Incrementar count {count}</button>

<h3>Stores (Componente pai)</h3>

Count store: {$countStore}

<button on:click={() => $countStore++}>Incrementar count store</button>

<NossoComponente {titulo} />

<style>
  h1 {
    color: red;
  }
</style>
