<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
  import MetaHead from "$lib/components/MetaHead.svelte";
  import SubHeader from "$lib/components/SubHeader.svelte";
  import Section from "$lib/components/Section.svelte";
  import AwardsSummary from "$lib/components/AwardsSummary.svelte";
  import AwardHighlightCard from "$lib/components/AwardHighlightCard.svelte";
  import SelectionsList from "$lib/components/SelectionsList.svelte";
  import SubFooter from "$lib/components/SubFooter.svelte";
</script>

<MetaHead 
  title="Awards and Official Selections"
  description="Emergence: Out of the Shadows has received 51 official festival selections, 7 awards, and recognition at Academy Award, BAFTA, and Canadian Screen Award qualifying festivals."
  canonical="/awards"
/>

<SubHeader 
  pageTitle="Awards and Official Selections" 
  breadcrumbs={[{ label: "Awards and Official Selections" }]}
/>

<!-- Introduction -->
<Section>
  <div class="max-w-4xl">
    <p class="text-lg text-gray-700 leading-relaxed mb-6">
      <em>{emergenceData.title}</em> has been recognized internationally for its powerful storytelling 
      and important social impact. The documentary has been selected for prestigious festivals worldwide, 
      earning critical acclaim and multiple awards across diverse categories.
    </p>
    
    <div class="bg-emerald-50 rounded-lg p-6">
      <p class="text-emerald-800 text-sm">
        <strong>Last Updated:</strong> {new Date(emergenceData.awardsSummary.updated).toLocaleDateString('en-US', { 
          year: 'numeric', 
          month: 'long', 
          day: 'numeric' 
        })}
      </p>
    </div>
  </div>
</Section>

<!-- Awards Summary -->
<Section className="bg-gray-50">
  <AwardsSummary summary={emergenceData.awardsSummary} />
</Section>

<!-- Highlights -->
<Section title="Highlights and Honours">
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    {#each emergenceData.awardsHighlights as highlight}
      <AwardHighlightCard {highlight} />
    {/each}
  </div>
</Section>

<!-- Full Official Selections List -->
<Section title="Complete Official Selections" className="bg-gray-50">
  <div class="mb-6">
    <p class="text-gray-700">
      Browse all {emergenceData.officialSelections.length} official festival selections. 
      Use the filters below to narrow down by category, outcome, or year.
    </p>
  </div>
  
  <SelectionsList selections={emergenceData.officialSelections} />
</Section>

<!-- Additional Recognition -->
<Section title="Additional Recognition">
  <div class="bg-white rounded-lg border border-gray-200 p-6">
    <h3 class="text-lg font-semibold text-gray-900 mb-4">Major Festival Selections</h3>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      {#each emergenceData.awardsSummary.otherMajorSelections as selection}
        <div class="text-sm text-gray-700 py-2 px-3 bg-gray-50 rounded-lg">
          {selection}
        </div>
      {/each}
    </div>
    
    <div class="mt-6 pt-6 border-t border-gray-200">
      <h4 class="font-medium text-gray-800 mb-2">Impact and Recognition</h4>
      <ul class="text-sm text-gray-600 space-y-1">
        <li>• Featured at {emergenceData.awardsSummary.countsByFestivalType.lgbtq} LGBTQ+ film festivals</li>
        <li>• Selected by {emergenceData.awardsSummary.countsByFestivalType.southAsian} South Asian film festivals</li>
        <li>• Recognized at {emergenceData.awardsSummary.countsByFestivalType.international} international festivals</li>
        <li>• Qualified for Academy Award, BAFTA, and Canadian Screen Award consideration</li>
      </ul>
    </div>
  </div>
</Section>

<SubFooter />