<script lang="ts">
  interface Props {
    title: string;
    runtime?: string;
    youtubeId: string;
    description?: string;
    className?: string;
  }
  
  let { title, runtime, youtubeId, description, className = "" }: Props = $props();
</script>

<div class="bg-white rounded-lg border border-gray-200 shadow-sm overflow-hidden {className}">
  <!-- Video Embed -->
  <div class="relative w-full aspect-video">
    <iframe
      src="https://www.youtube.com/embed/{youtubeId}"
      title={title}
      class="absolute inset-0 w-full h-full"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
      loading="lazy"
    ></iframe>
  </div>
  
  <!-- Content -->
  <div class="p-4">
    <div class="flex justify-between items-start mb-2">
      <h3 class="text-lg font-semibold text-gray-900 line-clamp-2">{title}</h3>
      {#if runtime}
        <span class="text-sm text-gray-500 ml-2 flex-shrink-0">{runtime}</span>
      {/if}
    </div>
    
    {#if description}
      <p class="text-gray-600 text-sm leading-relaxed">{description}</p>
    {/if}
  </div>
</div>

<style>
  .line-clamp-2 {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
</style>