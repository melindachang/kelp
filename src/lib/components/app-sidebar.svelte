<script lang="ts">
  import type { ComponentProps } from 'svelte'

  import * as Sidebar from '$lib/components/ui/sidebar'
  import * as DropdownMenu from '$lib/components/ui/dropdown-menu'
  import * as Collapsible from '$lib/components/ui/collapsible'

  import ModeToggle from '$lib/components/mode-toggle.svelte'

  import {
    Shrimp,
    House,
    Heart,
    LayoutDashboard,
    ChevronDown,
    Ellipsis,
    BookOpen,
    FolderKanban
  } from '@lucide/svelte'

  const menu_items = [
    { title: 'Home', url: '/', icon: House },
    { title: 'Favorites', url: '/favorites', icon: Heart },
    { title: 'Dashboard', url: '/dashboard', icon: LayoutDashboard }
  ]

  const libraries = [
    { title: 'Movies', url: '/libraries/movies' },
    { title: 'Music', url: '/libraries/music' }
  ]

  let { ...restProps }: ComponentProps<typeof Sidebar.Root> = $props()
</script>

<Sidebar.Root collapsible="offcanvas" {...restProps}>
  <Sidebar.Header>
    <Sidebar.Menu>
      <Sidebar.MenuItem>
        <Sidebar.MenuButton class="data-[slot=sidebar-menu-button]:!p-1.5">
          {#snippet child({ props })}
            <a href="/" {...props}>
              <Shrimp class="!size-5" />
              <span class="text-base font-semibold">Kelp</span>
            </a>
          {/snippet}
        </Sidebar.MenuButton>
      </Sidebar.MenuItem>
    </Sidebar.Menu>
  </Sidebar.Header>
  <Sidebar.Content>
    <Sidebar.Group>
      <Sidebar.GroupContent>
        <Sidebar.Input id="search" placeholder="Search..." />
      </Sidebar.GroupContent>
    </Sidebar.Group>
    <Sidebar.Group>
      <Sidebar.GroupLabel>General</Sidebar.GroupLabel>
      <Sidebar.GroupContent>
        <Sidebar.Menu>
          {#each menu_items as item (item.title)}
            <Sidebar.MenuItem>
              <Sidebar.MenuButton>
                {#snippet child({ props })}
                  <a href={item.url} {...props}>
                    <item.icon />
                    <span>{item.title}</span>
                  </a>
                {/snippet}
              </Sidebar.MenuButton>
            </Sidebar.MenuItem>
          {/each}
        </Sidebar.Menu>
      </Sidebar.GroupContent>
    </Sidebar.Group>
    <Sidebar.Group>
      <Sidebar.GroupLabel>Media</Sidebar.GroupLabel>
      <Sidebar.GroupContent>
        <Sidebar.Menu>
          <Collapsible.Root open class="group/collapsible">
            <Sidebar.MenuItem>
              <Collapsible.Trigger>
                {#snippet child({ props })}
                  <Sidebar.MenuButton {...props}>
                    <BookOpen />
                    <span>Libraries</span>
                    <ChevronDown
                      class="ml-auto transition-transform group-data-[state=open]/collapsible:rotate-180" />
                  </Sidebar.MenuButton>
                {/snippet}
              </Collapsible.Trigger>
              <Collapsible.Content>
                <Sidebar.MenuSub>
                  {#each libraries as item}
                    <Sidebar.MenuSubItem>
                      <Sidebar.MenuSubButton>
                        {#snippet child({ props })}
                          <a href={item.url} {...props}>
                            <span>{item.title}</span>
                          </a>
                        {/snippet}
                      </Sidebar.MenuSubButton>
                    </Sidebar.MenuSubItem>
                  {/each}
                </Sidebar.MenuSub>
              </Collapsible.Content>
            </Sidebar.MenuItem>
          </Collapsible.Root>
          <Sidebar.MenuItem>
            <Sidebar.MenuButton>
              <FolderKanban />
              <span>Metadata Manager</span>
            </Sidebar.MenuButton>
          </Sidebar.MenuItem>
        </Sidebar.Menu>
      </Sidebar.GroupContent>
    </Sidebar.Group>
  </Sidebar.Content>
  <Sidebar.Footer>
    <ModeToggle />
  </Sidebar.Footer>
</Sidebar.Root>
