<script lang="ts">
  import Header from "./layout/Header.svelte";
  import "../app.css";

</script>

<svelte:head>
  <title>Multiple Counter</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="app">
  <div class="text-center">
    <Header />
    <main>
      <slot/>
    </main>
    
  </div>
</div>

<style lang="postcss">
</style>
