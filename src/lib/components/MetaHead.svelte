<script lang="ts">
  interface Props {
    title: string;
    description: string;
    canonical?: string;
    ogImage?: string;
    ogType?: string;
    jsonLd?: Record<string, any>;
  }
  
  let { 
    title, 
    description, 
    canonical, 
    ogImage = "/favicon-96x96.png",
    ogType = "website",
    jsonLd 
  }: Props = $props();
  
  const fullTitle = title.includes("Emergence") ? title : `Emergence: Out of the Shadows — ${title}`;
</script>

<svelte:head>
  <!-- Title and Description -->
  <title>{fullTitle}</title>
  <meta name="description" content={description} />
  
  <!-- Canonical URL -->
  {#if canonical}
    <link rel="canonical" href={canonical} />
  {/if}
  
  <!-- Open Graph -->
  <meta property="og:title" content={fullTitle} />
  <meta property="og:description" content={description} />
  <meta property="og:image" content={ogImage} />
  <meta property="og:type" content={ogType} />
  {#if canonical}
    <meta property="og:url" content={canonical} />
  {/if}
  
  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content={fullTitle} />
  <meta name="twitter:description" content={description} />
  <meta name="twitter:image" content={ogImage} />
  
  <!-- JSON-LD -->
  {#if jsonLd}
    {@html `<script type="application/ld+json">${JSON.stringify(jsonLd)}</script>`}
  {/if}
</svelte:head>