<script lang="ts">
  import { page } from "$app/state";
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

<div id="subheader" class="sticky top-0 w-full z-40 -mt-2">
  <div
    class="flex items-center justify-between w-full px-8 py-2"
  >
    <!-- Movie Title Left -->
    <div
      class="text-white font-[Bebas_Neue] text-lg md:text-2xl tracking-wide uppercase font-semibold select-none"
    >
      {emergenceData.title}
    </div>
    <!-- Navigation Right (Plain HTML) -->
    <nav class="flex items-center space-x-2">
      {#each navigationItems as item}
        <div class="flex flex-col items-center overflow-hidden">
          <a
            href={item.href}
            class="group px-3 py-2 text-sm md:text-base font-[Poppins] text-white uppercase transition-all duration-200 w-full"
          >
            <span class="block">{item.label}</span>
            <span
              class="block h-0.5 bg-white rounded transition-all duration-200 ease-in-out w-0 group-hover:w-full"
            ></span>
          </a>
        </div>
      {/each}
    </nav>
  </div>
</div>
