<script lang="ts">
  interface Props {
    title?: string;
    children?: import("svelte").Snippet;
    className?: string;
  }
  
  let { title, children, className = "" }: Props = $props();
</script>

<section class="py-10 lg:py-14 {className}">
  <div class="max-w-7xl mx-auto px-6">
    {#if title}
      <h2 class="text-2xl lg:text-3xl font-bold text-gray-900 mb-8 tracking-tight">{title}</h2>
    {/if}
    
    <div class="prose prose-lg max-w-none">
      {@render children?.()}
    </div>
  </div>
</section>