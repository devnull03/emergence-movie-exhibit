<script lang="ts">
  interface AwardsSummary {
    updated: string;
    countsByFestivalType: Record<string, number>;
    countsByResult: Record<string, number>;
    qualifyingFestivals: Record<string, string[]>;
  }
  
  interface Props {
    summary: AwardsSummary;
  }
  
  let { summary }: Props = $props();
  
  const formatLabel = (key: string): string => {
    return key.replace(/([A-Z])/g, ' $1').replace(/^./, str => str.toUpperCase());
  };
</script>

<div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-8">
  <!-- Festival Types Summary -->
  <div class="bg-white rounded-lg border border-gray-200 p-6">
    <h3 class="text-lg font-semibold text-gray-900 mb-4">Festival Types</h3>
    <div class="grid grid-cols-2 gap-3">
      {#each Object.entries(summary.countsByFestivalType) as [type, count]}
        {#if type !== 'total'}
          <div class="flex justify-between items-center py-2 border-b border-gray-100">
            <span class="text-sm text-gray-700 capitalize">{formatLabel(type)}</span>
            <span class="font-medium text-emerald-600">{count}</span>
          </div>
        {/if}
      {/each}
      <div class="flex justify-between items-center py-2 border-t-2 border-gray-300 font-semibold">
        <span class="text-gray-900">Total</span>
        <span class="text-emerald-600">{summary.countsByFestivalType.total}</span>
      </div>
    </div>
  </div>
  
  <!-- Results Summary -->
  <div class="bg-white rounded-lg border border-gray-200 p-6">
    <h3 class="text-lg font-semibold text-gray-900 mb-4">Outcomes</h3>
    <div class="space-y-3">
      {#each Object.entries(summary.countsByResult) as [result, count]}
        {#if count > 0 && result !== 'totalOfficialSelections'}
          <div class="flex justify-between items-center py-2 border-b border-gray-100">
            <span class="text-sm text-gray-700">{formatLabel(result)}</span>
            <span class="font-medium text-emerald-600">{count}</span>
          </div>
        {/if}
      {/each}
      <div class="flex justify-between items-center py-2 border-t-2 border-gray-300 font-semibold">
        <span class="text-gray-900">Total Official Selections</span>
        <span class="text-emerald-600">{summary.countsByResult.totalOfficialSelections}</span>
      </div>
    </div>
  </div>
</div>

<!-- Qualifying Festivals -->
<div class="bg-white rounded-lg border border-gray-200 p-6 mb-8">
  <h3 class="text-lg font-semibold text-gray-900 mb-4">Award Qualifying Festivals</h3>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
    {#each Object.entries(summary.qualifyingFestivals) as [qualifier, festivals]}
      <div>
        <h4 class="font-medium text-gray-800 mb-2">
          <span class="inline-block bg-emerald-100 text-emerald-800 text-xs px-2 py-1 rounded-full">
            {formatLabel(qualifier)} Qualifying
          </span>
        </h4>
        <ul class="text-sm text-gray-600 space-y-1">
          {#each festivals as festival}
            <li>• {festival}</li>
          {/each}
        </ul>
      </div>
    {/each}
  </div>
</div>