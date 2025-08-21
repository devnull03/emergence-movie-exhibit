<script lang="ts">
  interface AwardHighlight {
    result: string;
    title: string;
    festival: string;
    date: string;
    location?: string;
    note?: string;
  }
  
  interface Props {
    highlight: AwardHighlight;
    className?: string;
  }
  
  let { highlight, className = "" }: Props = $props();
  
  const formatDate = (dateStr: string): string => {
    const date = new Date(dateStr);
    return date.toLocaleDateString('en-US', { 
      year: 'numeric', 
      month: 'long', 
      day: 'numeric' 
    });
  };
  
  const getResultColor = (result: string): string => {
    if (result.includes('Winner') || result.includes('Award')) return 'bg-yellow-100 text-yellow-800 border-yellow-200';
    if (result.includes('Finalist')) return 'bg-blue-100 text-blue-800 border-blue-200';
    if (result.includes('Opening') || result.includes('Closing')) return 'bg-purple-100 text-purple-800 border-purple-200';
    return 'bg-emerald-100 text-emerald-800 border-emerald-200';
  };
</script>

<div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6 {className}">
  <!-- Result Badge -->
  <div class="mb-3">
    <span class="inline-block px-3 py-1 text-xs font-medium rounded-full border {getResultColor(highlight.result)}">
      {highlight.result}
    </span>
  </div>
  
  <!-- Title -->
  <h3 class="text-lg font-semibold text-gray-900 mb-2 leading-tight">
    {highlight.title}
  </h3>
  
  <!-- Festival -->
  <p class="text-gray-700 font-medium mb-2">
    {highlight.festival}
  </p>
  
  <!-- Date and Location -->
  <div class="text-sm text-gray-500 mb-3">
    <p>{formatDate(highlight.date)}</p>
    {#if highlight.location}
      <p>{highlight.location}</p>
    {/if}
  </div>
  
  <!-- Note -->
  {#if highlight.note}
    <p class="text-sm text-gray-600 italic border-l-4 border-emerald-200 pl-3">
      {highlight.note}
    </p>
  {/if}
</div>