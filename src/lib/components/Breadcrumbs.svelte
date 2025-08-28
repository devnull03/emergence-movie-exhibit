<script lang="ts">
  import { page } from "$app/stores";
  import * as Breadcrumb from "$lib/components/ui/breadcrumb";

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

<Breadcrumb.Root>
  <Breadcrumb.List>
    {#each finalBreadcrumbs as breadcrumb, index}
      <Breadcrumb.Item>
        {#if breadcrumb.href}
          <Breadcrumb.Link href={breadcrumb.href}>
            {breadcrumb.label}
          </Breadcrumb.Link>
        {:else}
          <Breadcrumb.Page>
            {breadcrumb.label}
          </Breadcrumb.Page>
        {/if}
      </Breadcrumb.Item>
      {#if index < finalBreadcrumbs.length - 1}
        <Breadcrumb.Separator />
      {/if}
    {/each}
  </Breadcrumb.List>
</Breadcrumb.Root>
