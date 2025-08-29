<script lang="ts">
  import type { Component } from 'svelte'
  import * as Sidebar from '$lib/components/ui/sidebar/index.js'
  import * as DropdownMenu from '$lib/components/ui/dropdown-menu/index.js'
  import {
    RefreshCwIcon,
    EllipsisIcon,
    FolderCogIcon,
    Trash2Icon
  } from '@lucide/svelte'

  let {
    libraries
  }: { libraries: { name: string; url: string; icon: Component }[] } = $props()

  const sidebar = Sidebar.useSidebar()
</script>

<Sidebar.Group class="group-data-[collapsible=icon]:hidden">
  <Sidebar.GroupLabel>Libraries</Sidebar.GroupLabel>
  <Sidebar.Menu>
    {#each libraries as item (item.name)}
      <Sidebar.MenuItem>
        <Sidebar.MenuButton>
          {#snippet child({ props })}
            <a href={item.url} {...props}>
              <item.icon />
              <span>{item.name}</span>
            </a>
          {/snippet}
        </Sidebar.MenuButton>
        <DropdownMenu.Root>
          <DropdownMenu.Trigger>
            {#snippet child({ props })}
              <Sidebar.MenuAction showOnHover {...props}>
                <EllipsisIcon />
                <span class="sr-only">More</span>
              </Sidebar.MenuAction>
            {/snippet}
          </DropdownMenu.Trigger>
          <DropdownMenu.Content
            class="w-48"
            side={sidebar.isMobile ? 'bottom' : 'right'}
            align={sidebar.isMobile ? 'end' : 'start'}>
            <DropdownMenu.Item>
              <RefreshCwIcon class="text-muted-foreground" />
              <span>Refresh Metadata</span>
            </DropdownMenu.Item>
            <DropdownMenu.Item>
              <FolderCogIcon class="text-muted-foreground" />
              <span>Edit Library</span>
            </DropdownMenu.Item>
            <DropdownMenu.Separator />
            <DropdownMenu.Item>
              <Trash2Icon class="text-muted-foreground" />
              <span>Delete Library</span>
            </DropdownMenu.Item>
          </DropdownMenu.Content>
        </DropdownMenu.Root>
      </Sidebar.MenuItem>
    {/each}
    <Sidebar.MenuItem>
      <Sidebar.MenuButton>
        <EllipsisIcon />
        <span>More</span>
      </Sidebar.MenuButton>
    </Sidebar.MenuItem>
  </Sidebar.Menu>
</Sidebar.Group>
