<script lang="ts">
  interface OfficialSelection {
    category: string;
    festival: string;
    qualifier?: string;
    premiere?: string;
    dates: string;
    city: string;
    region: string;
    country: string;
    format?: string;
    outcome?: string;
    note?: string;
  }
  
  interface Props {
    selections: OfficialSelection[];
  }
  
  let { selections }: Props = $props();
  
  let categoryFilter = $state('all');
  let outcomeFilter = $state('all');
  let yearFilter = $state('all');
  
  // Extract unique values for filters
  const categories = [...new Set(selections.map(s => s.category))].sort();
  const outcomes = [...new Set(selections.filter(s => s.outcome).map(s => s.outcome!))].sort();
  const years = [...new Set(selections.map(s => s.dates.substring(0, 4)))].sort().reverse();
  
  // Filter selections based on current filters
  const filteredSelections = $derived(() => {
    return selections.filter(selection => {
      const categoryMatch = categoryFilter === 'all' || selection.category === categoryFilter;
      const outcomeMatch = outcomeFilter === 'all' || selection.outcome === outcomeFilter;
      const yearMatch = yearFilter === 'all' || selection.dates.startsWith(yearFilter);
      
      return categoryMatch && outcomeMatch && yearMatch;
    }).sort((a, b) => b.dates.localeCompare(a.dates)); // Most recent first
  });
  
  const formatDate = (dateStr: string): string => {
    // Handle date ranges
    if (dateStr.includes(' to ')) {
      const [start, end] = dateStr.split(' to ');
      const startDate = new Date(start);
      const endDate = new Date(end);
      return `${startDate.toLocaleDateString('en-US', { month: 'short', day: 'numeric' })} - ${endDate.toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' })}`;
    }
    
    // Handle single dates
    const date = new Date(dateStr);
    return date.toLocaleDateString('en-US', { 
      year: 'numeric', 
      month: 'short', 
      day: 'numeric' 
    });
  };
  
  const getCategoryColor = (category: string): string => {
    const colors: Record<string, string> = {
      'QUEER': 'bg-rainbow-100 text-rainbow-800 border-rainbow-200',
      'SOUTH ASIAN': 'bg-orange-100 text-orange-800 border-orange-200',
      'ASIAN': 'bg-red-100 text-red-800 border-red-200',
      'DOCUMENTARY': 'bg-blue-100 text-blue-800 border-blue-200',
      'INTERNATIONAL': 'bg-green-100 text-green-800 border-green-200',
      'BIPOC': 'bg-purple-100 text-purple-800 border-purple-200',
      "WOMEN'S": 'bg-pink-100 text-pink-800 border-pink-200',
      'OTHER': 'bg-gray-100 text-gray-800 border-gray-200'
    };
    return colors[category] || colors['OTHER'];
  };
  
  const getOutcomeColor = (outcome: string): string => {
    if (outcome.includes('Winner') || outcome.includes('Award')) return 'bg-yellow-100 text-yellow-800';
    if (outcome.includes('Finalist')) return 'bg-blue-100 text-blue-800';
    if (outcome.includes('Opening') || outcome.includes('Closing')) return 'bg-purple-100 text-purple-800';
    return 'bg-emerald-100 text-emerald-800';
  };
</script>

<!-- Filters -->
<div class="bg-white rounded-lg border border-gray-200 p-4 mb-6">
  <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
    <!-- Category Filter -->
    <div>
      <label for="category" class="block text-sm font-medium text-gray-700 mb-1">Category</label>
      <select 
        id="category"
        bind:value={categoryFilter} 
        class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500"
      >
        <option value="all">All Categories</option>
        {#each categories as category}
          <option value={category}>{category.toLowerCase().replace(/'/g, '').split(' ').map(w => w.charAt(0).toUpperCase() + w.slice(1)).join(' ')}</option>
        {/each}
      </select>
    </div>
    
    <!-- Outcome Filter -->
    <div>
      <label for="outcome" class="block text-sm font-medium text-gray-700 mb-1">Outcome</label>
      <select 
        id="outcome"
        bind:value={outcomeFilter} 
        class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500"
      >
        <option value="all">All Outcomes</option>
        {#each outcomes as outcome}
          <option value={outcome}>{outcome}</option>
        {/each}
      </select>
    </div>
    
    <!-- Year Filter -->
    <div>
      <label for="year" class="block text-sm font-medium text-gray-700 mb-1">Year</label>
      <select 
        id="year"
        bind:value={yearFilter} 
        class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500"
      >
        <option value="all">All Years</option>
        {#each years as year}
          <option value={year}>{year}</option>
        {/each}
      </select>
    </div>
  </div>
  
  <div class="mt-3 text-sm text-gray-600">
    Showing {filteredSelections().length} of {selections.length} selections
  </div>
</div>

<!-- Selections List -->
<div class="bg-white rounded-lg border border-gray-200 overflow-hidden">
  {#if filteredSelections().length === 0}
    <div class="p-8 text-center text-gray-500">
      <p>No selections match the current filters.</p>
    </div>
  {:else}
    <div class="divide-y divide-gray-200">
      {#each filteredSelections() as selection, i}
        <div class="p-4 hover:bg-gray-50 transition-colors">
          <div class="flex flex-wrap items-start justify-between gap-4">
            <div class="flex-1 min-w-0">
              <!-- Festival Name -->
              <h3 class="text-lg font-medium text-gray-900 mb-2">
                {selection.festival}
              </h3>
              
              <!-- Badges -->
              <div class="flex flex-wrap gap-2 mb-2">
                <span class="inline-block px-2 py-1 text-xs font-medium rounded-full border {getCategoryColor(selection.category)}">
                  {selection.category.toLowerCase().replace(/'/g, '').split(' ').map(w => w.charAt(0).toUpperCase() + w.slice(1)).join(' ')}
                </span>
                
                {#if selection.qualifier}
                  <span class="inline-block px-2 py-1 text-xs font-medium rounded-full bg-indigo-100 text-indigo-800 border border-indigo-200">
                    {selection.qualifier}
                  </span>
                {/if}
                
                {#if selection.premiere}
                  <span class="inline-block px-2 py-1 text-xs font-medium rounded-full bg-teal-100 text-teal-800 border border-teal-200">
                    {selection.premiere}
                  </span>
                {/if}
                
                {#if selection.format}
                  <span class="inline-block px-2 py-1 text-xs font-medium rounded-full bg-gray-100 text-gray-700 border border-gray-200">
                    {selection.format}
                  </span>
                {/if}
              </div>
              
              <!-- Location and Date -->
              <div class="text-sm text-gray-600 space-y-1">
                <p>
                  📍 {selection.city}{selection.region ? `, ${selection.region}` : ''}, {selection.country}
                </p>
                <p>📅 {formatDate(selection.dates)}</p>
              </div>
              
              <!-- Note -->
              {#if selection.note}
                <p class="mt-2 text-sm text-gray-600 italic">
                  {selection.note}
                </p>
              {/if}
            </div>
            
            <!-- Outcome -->
            {#if selection.outcome}
              <div class="flex-shrink-0">
                <span class="inline-block px-3 py-1 text-sm font-medium rounded-full {getOutcomeColor(selection.outcome)}">
                  {selection.outcome}
                </span>
              </div>
            {/if}
          </div>
        </div>
      {/each}
    </div>
  {/if}
</div>