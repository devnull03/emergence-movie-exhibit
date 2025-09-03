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
  class="sticky top-0 bg-white/80 backdrop-blur-md border-b border-border/20 -mt-2 z-40"
>
  <div class="md:max-w-6xl w-full mx-auto px-4 py-1.5">
    <NavigationMenu.Root>
      <NavigationMenu.List class="flex items-center space-x-1">
        {#each navigationItems as item}
          <NavigationMenu.Item>
            <NavigationMenu.Link
              href={item.href}
              class="px-2.5 py-1.5 text-xs font-medium transition-all duration-200 {item.isActive
                ? 'text-foreground border-b border-primary'
                : 'text-muted-foreground hover:text-foreground hover:bg-accent/30 rounded-md'}"
            >
              {item.label}
            </NavigationMenu.Link>
          </NavigationMenu.Item>
        {/each}
      </NavigationMenu.List>
    </NavigationMenu.Root>
  </div>
</div>
