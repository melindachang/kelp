<script lang="ts">
  import { page } from '$app/state'
  import { type Component } from 'svelte'

  import HomeFill16 from '$lib/icons/HomeFill16.svelte'
  import HeartFill16 from '$lib/icons/HeartFill16.svelte'
  import Cache16 from '$lib/icons/Cache16.svelte'
  import Apps16 from '$lib/icons/Apps16.svelte'
  import ChevronDown16 from '$lib/icons/ChevronDown16.svelte'

  import SidebarIcon from '$lib/components/SidebarIcon.svelte'

  type Link = { name: string; path: string; icon: Component | undefined }

  const global_links: Link[] = [
    { name: 'Home', path: '/', icon: HomeFill16 },
    { name: 'Favorites', path: '/favorites', icon: HeartFill16 },
    { name: 'Dashboard', path: '/dashboard', icon: Cache16 }
  ]

  const temp_links: Link[] = [
    { name: 'Movies', path: '/libraries/movies', icon: undefined },
    { name: 'Music', path: '/libraries/music', icon: undefined }
  ]

  let showLibraries = $state(true)
</script>

{#snippet link(
  name: string,
  href: string,
  Icon: Component | undefined = undefined
)}
  <a
    class={[
      'sidebar__link',
      href.startsWith('/libraries/') && 'sidebar__link--lvl-2',
      page.url.pathname === href && 'sidebar__link--active'
    ]}
    {href}
    ><span class="sidebar__link__name"
      >{#if Icon}<SidebarIcon {Icon} />{/if}
      {name}</span
    ></a>
{/snippet}

<div class="sidebar">
  <div class="sidebar__content">
    <div class="sidebar__logo">Kelp</div>
    <div class="sidebar__search">
      <input type="text" placeholder="Search..." />
    </div>
    <div class="sidebar__links">
      {#each global_links as l}
        {@render link(l.name, l.path, l.icon)}
      {/each}

      <!-- 'LIBRARIES' DROPDOWN -->

      <button
        class="sidebar__link--dropdown"
        onclick={() => (showLibraries = !showLibraries)}>
        <span class="sidebar__link__name"
          ><SidebarIcon Icon={Apps16} /> Libraries</span>
        <span
          class={[
            'sidebar__link__icon--dropdown',
            showLibraries && 'sidebar__link__icon--dropdown--open'
          ]}><ChevronDown16 /></span>
      </button>

      {#if showLibraries}
        <div class="sidebar__link--dropdown__body">
          {#each temp_links as l}
            {@render link(l.name, l.path, l.icon)}
          {/each}
        </div>
      {/if}
    </div>
  </div>
</div>

<style lang="scss">
  @use '../styles/_mixins';

  .sidebar {
    position: fixed;
    height: 100%;
    z-index: 2;
    padding: var(--pd-body) 0 var(--pd-body) var(--pd-body);

    &__content {
      @extend %card-base;

      height: 100%;
      display: flex;
      flex-direction: column;
      gap: 3.2rem;
    }

    &__logo {
      color: var(--clr-white);
    }

    &__search {
      input {
        @extend %input-text;
        width: var(--width-search);
      }
    }

    &__links {
      display: flex;
      flex-direction: column;
      gap: 0.8rem;
    }

    &__link {
      cursor: pointer;
      font-size: 1.5rem;
      padding: var(--pd-input);
      border: mixins.$border-faux;
      border-radius: var(--rounding-sm);
      transition: color 0.2s ease;

      &__name {
        display: flex;
        align-items: center;
        gap: 0.8rem;
      }

      &:hover {
        color: var(--clr-white);
        .sidebar__link__icon {
          fill: var(--clr-white);
        }
      }

      &--dropdown {
        @extend .sidebar__link;

        display: flex;
        justify-content: space-between;

        &__body {
          display: flex;
          flex-direction: column;
          margin-left: 3.2rem;
          position: relative;

          &::after {
            position: absolute;
            width: 1px;
            content: '';
            left: -1.2rem;
            top: 6px;
            bottom: 6px;
            background-color: hsla(0, 0%, 100%, 0.2);
          }
        }
      }

      &--active {
        @extend %input-button;
        border: mixins.$border-base;

        .sidebar__link__icon {
          fill: var(--clr-white);
        }
      }

      &__icon {
        fill: var(--clr-white);
        transition: fill 0.2s ease;

        &--dropdown {
          @extend .sidebar__link__icon;

          display: flex;
          align-items: center;

          &--open {
            transform: rotate(180deg);
          }
        }
      }
    }
  }
</style>
