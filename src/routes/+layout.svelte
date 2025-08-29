<script lang="ts">
  import '../app.css'

  import AppSidebar from '$lib/components/app-sidebar.svelte'
  import SiteHeader from '$lib/components/site-header.svelte'
  import * as Sidebar from '$lib/components/ui/sidebar'

  import { ModeWatcher } from 'mode-watcher'

  let { children } = $props()
</script>

<ModeWatcher />

<div class="[--header-height:calc(--spacing(14))]">
  <Sidebar.Provider class="flex flex-col">
    <SiteHeader />
    <div class="flex flex-1">
      <AppSidebar />
      <Sidebar.Inset>
        <main>{@render children()}</main>
      </Sidebar.Inset>
    </div>
  </Sidebar.Provider>
</div>
