<script lang="ts">
  import Breadcrumbs from "./Breadcrumbs.svelte";
  import emergenceData from "$lib/content/films/emergence.json";

  interface Props {
    pageTitle?: string;
    showRightsNotice?: boolean;
  }

  let { pageTitle = "", showRightsNotice = true }: Props = $props();
</script>

<div
  class="sticky top-0 z-50 bg-white/95 backdrop-blur-sm border-b border-border"
>
  <div class="max-w-6xl mx-auto px-4 sm:px-6 py-3">
    <div class="flex items-center justify-between">
      <div class="flex items-center space-x-4">
        <Breadcrumbs />
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
