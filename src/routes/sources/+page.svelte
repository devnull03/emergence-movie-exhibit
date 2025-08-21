<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
  import MetaHead from "$lib/components/MetaHead.svelte";
  import SubHeader from "$lib/components/SubHeader.svelte";
  import Section from "$lib/components/Section.svelte";
  import SubFooter from "$lib/components/SubFooter.svelte";
  import { Button } from "$lib/components/ui/button";
</script>

<MetaHead 
  title="Sources and Credits"
  description="Official sources, credits, and attribution information for Emergence: Out of the Shadows documentary"
  canonical="/sources"
/>

<SubHeader 
  pageTitle="Sources and Credits" 
  breadcrumbs={[{ label: "Sources and Credits" }]}
/>

<!-- Introduction -->
<Section>
  <div class="max-w-4xl">
    <p class="text-lg text-gray-700 leading-relaxed mb-8">
      This exhibit is presented in partnership with the South Asian Canadian Digital Archive (SACDA). 
      All content, materials, and information are sourced from official channels and archive partners.
    </p>
  </div>
</Section>

<!-- Official Sources -->
<Section title="Official Sources" className="bg-gray-50">
  <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
    <!-- Official Website -->
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <div class="flex items-center mb-4">
        <svg class="h-6 w-6 text-emerald-600 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9v-9m0-9v9" />
        </svg>
        <h3 class="text-lg font-semibold text-gray-900">Official Film Website</h3>
      </div>
      <p class="text-gray-600 mb-4">
        The primary source for all film information, cast and crew details, and official materials.
      </p>
      <Button variant="outline" class="w-full">
        <a href={emergenceData.sources.officialSite} target="_blank" rel="noopener noreferrer" class="no-underline">
          Visit emergencefilm.net
        </a>
      </Button>
    </div>
    
    <!-- Archive Listing -->
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <div class="flex items-center mb-4">
        <svg class="h-6 w-6 text-emerald-600 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10" />
        </svg>
        <h3 class="text-lg font-semibold text-gray-900">QT Sikh Archive</h3>
      </div>
      <p class="text-gray-600 mb-4">
        Partner archive providing scholarly context and historical documentation.
      </p>
      <Button variant="outline" class="w-full">
        <a href={emergenceData.sources.archiveListing} target="_blank" rel="noopener noreferrer" class="no-underline">
          View Archive Entry
        </a>
      </Button>
    </div>
  </div>
</Section>

<!-- Educational Resources -->
<Section title="Educational Resources">
  <div class="bg-white rounded-lg border border-gray-200 p-6">
    <h3 class="text-lg font-semibold text-gray-900 mb-4">Teaching Materials</h3>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <div>
        <h4 class="font-medium text-gray-800 mb-2">Discussion Guide</h4>
        <p class="text-gray-600 text-sm mb-3">
          Comprehensive educational resource designed for classroom use and community screenings.
        </p>
        <Button variant="outline" size="sm">
          <a href={emergenceData.teacherGuide.href} target="_blank" rel="noopener noreferrer" class="no-underline">
            Download Guide (PDF)
          </a>
        </Button>
      </div>
      
      <div>
        <h4 class="font-medium text-gray-800 mb-2">Video Resources</h4>
        <p class="text-gray-600 text-sm mb-3">
          Multiple language versions and cast spotlights available for educational use.
        </p>
        <Button variant="outline" size="sm">
          <a href="/film" class="no-underline">View All Versions</a>
        </Button>
      </div>
    </div>
  </div>
</Section>

<!-- Credits and Attribution -->
<Section title="Credits and Attribution" className="bg-gray-50">
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
    <!-- Exhibit Credits -->
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">Exhibit Information</h3>
      <dl class="space-y-3 text-sm">
        <div>
          <dt class="font-medium text-gray-700">Presented by:</dt>
          <dd class="text-gray-600">South Asian Canadian Digital Archive (SACDA)</dd>
        </div>
        <div>
          <dt class="font-medium text-gray-700">Content Source:</dt>
          <dd class="text-gray-600">Official film materials and partner archives</dd>
        </div>
        <div>
          <dt class="font-medium text-gray-700">Educational Partnership:</dt>
          <dd class="text-gray-600">QT Sikh Archive</dd>
        </div>
        <div>
          <dt class="font-medium text-gray-700">Platform:</dt>
          <dd class="text-gray-600">Digital Exhibits Platform</dd>
        </div>
      </dl>
    </div>
    
    <!-- Acknowledgments -->
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">Acknowledgments</h3>
      <p class="text-gray-600 text-sm leading-relaxed mb-4">
        Special thanks to the filmmakers, cast members, and community partners who made this 
        documentary possible and supported the creation of this educational exhibit.
      </p>
      <p class="text-gray-600 text-sm leading-relaxed">
        This exhibit is made possible through the generous support of community donors 
        and institutional partners committed to preserving and sharing South Asian Canadian stories.
      </p>
    </div>
  </div>
</Section>

<!-- Donation and Support -->
<Section title="Support Our Work">
  <div class="bg-emerald-50 rounded-lg p-8 text-center">
    <h3 class="text-xl font-semibold text-gray-900 mb-4">Help Preserve Our Stories</h3>
    <p class="text-gray-700 mb-6 max-w-2xl mx-auto">
      The South Asian Canadian Digital Archive depends on community support to continue 
      documenting and sharing important stories like <em>Emergence: Out of the Shadows</em>. 
      Your contribution helps us maintain and expand our digital exhibits and educational resources.
    </p>
    <div class="flex flex-col sm:flex-row gap-4 justify-center">
      <Button>
        <a href="https://sacda.ca/donate" target="_blank" rel="noopener noreferrer" class="text-white no-underline">
          Support SACDA
        </a>
      </Button>
      <Button variant="outline">
        <a href="https://sacda.ca" target="_blank" rel="noopener noreferrer" class="no-underline">
          Learn More About SACDA
        </a>
      </Button>
    </div>
  </div>
</Section>

<SubFooter />