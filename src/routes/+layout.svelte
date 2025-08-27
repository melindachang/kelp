<script lang="ts">
  import '$lib/styles/main.scss'

  import Sidebar from '$lib/components/Sidebar.svelte'

  let { children } = $props()
</script>

<svelte:head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
</svelte:head>

<main class="container">
  <div class="sidebar">
    <Sidebar />
  </div>
  <div class="content">
    {@render children()}
  </div>
</main>

<style lang="scss">
</style>
