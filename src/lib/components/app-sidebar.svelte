<script lang="ts" module>
  import {
    SquareTerminalIcon,
    BotIcon,
    BookOpenIcon,
    Settings2Icon,
    LifeBuoyIcon,
    SendIcon,
    FilmIcon,
    MusicIcon,
    TvIcon,
    ShrimpIcon
  } from '@lucide/svelte'

  const data = {
    user: {
      name: 'shadcn',
      email: 'm@example.com',
      avatar: '/avatars/shadcn.jpg'
    },
    navMain: [
      {
        title: 'Playground',
        url: '#',
        icon: SquareTerminalIcon,
        isActive: true,
        items: [
          { title: 'History', url: '#' },
          { title: 'Starred', url: '#' },
          { title: 'Settings', url: '#' }
        ]
      },
      {
        title: 'Models',
        url: '#',
        icon: BotIcon,
        items: [
          { title: 'Genesis', url: '#' },
          { title: 'Explorer', url: '#' },
          { title: 'Quantum', url: '#' }
        ]
      },
      {
        title: 'Documentation',
        url: '#',
        icon: BookOpenIcon,
        items: [
          { title: 'Introduction', url: '#' },
          { title: 'Get Started', url: '#' },
          { title: 'Tutorials', url: '#' },
          { title: 'Changelog', url: '#' }
        ]
      },
      {
        title: 'Settings',
        url: '#',
        icon: Settings2Icon,
        items: [
          { title: 'General', url: '#' },
          { title: 'Team', url: '#' },
          { title: 'Billing', url: '#' },
          { title: 'Limits', url: '#' }
        ]
      }
    ],
    navSecondary: [
      { title: 'Support', url: '#', icon: LifeBuoyIcon },
      { title: 'Feedback', url: '#', icon: SendIcon }
    ],
    libraries: [
      { name: 'Movies', url: '#', icon: FilmIcon },
      { name: 'Music', url: '#', icon: MusicIcon },
      { name: 'Shows', url: '#', icon: TvIcon }
    ]
  }
</script>

<script lang="ts">
  import type { ComponentProps } from 'svelte'
  import * as Sidebar from '$lib/components/ui/sidebar/index.js'
  import NavMain from './nav-main.svelte'
  import NavLibraries from './nav-libraries.svelte'
  import NavSecondary from './nav-secondary.svelte'
  import NavUser from './nav-user.svelte'

  let {
    ref = $bindable(null),
    ...restProps
  }: ComponentProps<typeof Sidebar.Root> = $props()
</script>

<Sidebar.Root
  class="top-(--header-height) h-[calc(100svh-var(--header-height))]!"
  {...restProps}>
  <Sidebar.Header>
    <Sidebar.Menu>
      <Sidebar.MenuItem>
        <Sidebar.MenuButton size="lg">
          {#snippet child({ props })}
            <a href="##" {...props}>
              <div
                class="flex aspect-square size-8 items-center justify-center rounded-lg bg-sidebar-primary text-sidebar-primary-foreground">
                <ShrimpIcon class="size-4" />
              </div>
              <div class="grid flex-1 text-left text-sm leading-tight">
                <span class="truncate font-medium">Kelp</span>
                <span class="truncate text-xs">v0.1.0</span>
              </div>
            </a>
          {/snippet}
        </Sidebar.MenuButton>
      </Sidebar.MenuItem>
    </Sidebar.Menu>
  </Sidebar.Header>
  <Sidebar.Content>
    <NavMain items={data.navMain} />
    <NavLibraries libraries={data.libraries} />
    <NavSecondary items={data.navSecondary} class="mt-auto" />
  </Sidebar.Content>
  <Sidebar.Footer>
    <NavUser user={data.user} />
  </Sidebar.Footer>
</Sidebar.Root>
