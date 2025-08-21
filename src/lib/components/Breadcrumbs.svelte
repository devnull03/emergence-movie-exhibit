<script lang="ts">
  import { page } from "$app/stores";

  interface BreadcrumbItem {
    label: string;
    href?: string;
  }

  interface Props {
    items?: BreadcrumbItem[];
    showHome?: boolean;
  }

  let { items = [], showHome = true }: Props = $props();

  const generateAutoBreadcrumbs = $derived(() => {
    const pathname = $page.url.pathname;
    const segments = pathname.split("/").filter(Boolean);

    const breadcrumbs: BreadcrumbItem[] = [];

    if (showHome) {
      breadcrumbs.push({ label: "Home", href: "/" });
    }

    if (segments.length > 0) {
      let currentPath = "";
      segments.forEach((segment) => {
        currentPath += `/${segment}`;
        const label =
          segment.charAt(0).toUpperCase() + segment.slice(1).replace("-", " ");
        breadcrumbs.push({
          label,
          href: currentPath === pathname ? undefined : currentPath,
        });
      });
    }

    return breadcrumbs;
  });

  const finalBreadcrumbs = $derived(
    items.length > 0 ? items : generateAutoBreadcrumbs()
  );
</script>

<nav aria-label="Breadcrumb" class="flex items-center space-x-2 text-sm">
  {#each finalBreadcrumbs as breadcrumb, index}
    <div class="flex items-center">
      {#if index > 0}
        <span class="mx-2 text-muted-foreground">/</span>
      {/if}
      {#if breadcrumb.href}
        <a
          href={breadcrumb.href}
          class="text-muted-foreground hover:text-foreground transition-colors hover:underline underline-offset-2"
        >
          {breadcrumb.label}
        </a>
      {:else}
        <span class="text-foreground font-medium">
          {breadcrumb.label}
        </span>
      {/if}
    </div>
  {/each}
</nav>
