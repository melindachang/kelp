<script lang="ts">
  import type { Component } from 'svelte'
  let { Icon }: { Icon: Component } = $props()
</script>

<div class="container">
  <div class="icon">
    <Icon width={14} height={14} />
  </div>
</div>

<style lang="scss">
  @use '../styles/_mixins';
  .container {
    border-radius: 4px;
    border: mixins.$border-base;
    padding: 6px;

    background-color: var(--bg-card-emph);
  }

  .icon {
    fill: var(--clr-gray-light);
  }
</style>
