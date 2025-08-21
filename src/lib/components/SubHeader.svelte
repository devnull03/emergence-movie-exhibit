<script lang="ts">
  interface Props {
    pageTitle: string;
    breadcrumbs?: Array<{ label: string; href?: string }>;
  }
  
  let { pageTitle, breadcrumbs = [] }: Props = $props();
</script>

<header class="bg-white border-b border-gray-200 py-4 px-6">
  <div class="max-w-7xl mx-auto">
    <!-- Breadcrumbs -->
    {#if breadcrumbs.length > 0}
      <nav class="flex mb-2" aria-label="Breadcrumb">
        <ol class="inline-flex items-center space-x-1 md:space-x-3">
          <li class="inline-flex items-center">
            <a href="/" class="inline-flex items-center text-sm font-medium text-gray-700 hover:text-emerald-600">
              <svg class="w-3 h-3 mr-2.5" fill="currentColor" viewBox="0 0 20 20">
                <path d="m19.707 9.293-2-2-7-7a1 1 0 0 0-1.414 0l-7 7-2 2a1 1 0 0 0 1.414 1.414L2 10.414V18a2 2 0 0 0 2 2h3a1 1 0 0 0 1-1v-4a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1v4a1 1 0 0 0 1 1h3a2 2 0 0 0 2-2v-7.586l.293.293a1 1 0 0 0 1.414-1.414Z"/>
              </svg>
              Home
            </a>
          </li>
          {#each breadcrumbs as crumb, i}
            <li>
              <div class="flex items-center">
                <svg class="w-3 h-3 text-gray-400 mx-1" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M7.21 14.77a.75.75 0 01.02-1.06L11.168 10 7.23 6.29a.75.75 0 111.04-1.08l4.5 4.25a.75.75 0 010 1.08l-4.5 4.25a.75.75 0 01-1.06-.02z" clip-rule="evenodd"/>
                </svg>
                {#if crumb.href && i < breadcrumbs.length - 1}
                  <a href={crumb.href} class="ml-1 text-sm font-medium text-gray-700 hover:text-emerald-600">
                    {crumb.label}
                  </a>
                {:else}
                  <span class="ml-1 text-sm font-medium text-gray-500">
                    {crumb.label}
                  </span>
                {/if}
              </div>
            </li>
          {/each}
        </ol>
      </nav>
    {/if}
    
    <!-- Page Title -->
    <h1 class="text-3xl font-bold text-gray-900">{pageTitle}</h1>
  </div>
</header>