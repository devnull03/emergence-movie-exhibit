<script lang="ts">
  import { page } from "$app/state";
  import * as NavigationMenu from "$lib/components/ui/navigation-menu";
  import emergenceData from "$lib/content/films/emergence.json";

  interface Props {
    pageTitle?: string;
    showRightsNotice?: boolean;
  }

  let { pageTitle = "" }: Props = $props();

  // Generate navigation items based on current route
  const navigationItems = $derived.by(() => {
    const pathname = page.url.pathname;
    const items = [
      { label: "Home", href: "/" },
      { label: "Awards", href: "/awards" },
      { label: "Cast & Crew", href: "/cast" },
      { label: "Sources", href: "/sources" },
    ];

    return items.map((item) => ({
      ...item,
      isActive: pathname === item.href,
    }));
  });
</script>

<div
  id="subheader"
  class="sticky top-0 bg-white/95 backdrop-blur-sm border-b border-border"
>
  <div class="max-w-6xl mx-auto px-4 sm:px-6 py-3">
    <div class="flex items-center justify-between">
      <div class="flex items-center space-x-4">
        <NavigationMenu.Root>
          <NavigationMenu.List class="space-x-2">
            {#each navigationItems as item}
              <NavigationMenu.Item>
                <NavigationMenu.Link
                  href={item.href}
                  class="px-3 py-2 text-sm font-medium rounded-md transition-colors {item.isActive
                    ? 'bg-primary text-primary-foreground'
                    : 'text-muted-foreground hover:text-foreground hover:bg-accent'}"
                >
                  {item.label}
                </NavigationMenu.Link>
              </NavigationMenu.Item>
            {/each}
          </NavigationMenu.List>
        </NavigationMenu.Root>

        <!-- Sticky title container for GSAP animation -->
        <div
          id="sticky-title-container"
          class="opacity-0 transition-opacity duration-300"
        >
          <h1 class="text-xl font-bold text-foreground">
            Emergence: Out of the Shadows
          </h1>
        </div>
      </div>

      {#if pageTitle}
        <h1 class="text-2xl font-bold text-foreground hidden md:block">
          {pageTitle}
        </h1>
      {/if}
    </div>
    <!-- 
    {#if showRightsNotice}
      <div
        class="mt-3 px-4 py-2 bg-amber-50 border border-amber-200 rounded-lg text-sm text-amber-800"
      >
        <span class="font-medium">⚠ Usage Notice:</span>
        {emergenceData.rights.notice}
      </div>
    {/if} -->
  </div>
</div>
