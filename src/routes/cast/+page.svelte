<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
  import MetaHead from "$lib/components/MetaHead.svelte";
  import SubHeader from "$lib/components/SubHeader.svelte";
  import Section from "$lib/components/Section.svelte";
  import VideoCard from "$lib/components/VideoCard.svelte";
  import SubFooter from "$lib/components/SubFooter.svelte";
  import { Button } from "$lib/components/ui/button";
</script>

<MetaHead 
  title="Cast Spotlights"
  description="Personal stories from Amar, Jag, and Kayden - the cast of Emergence: Out of the Shadows documentary"
  canonical="/cast"
/>

<SubHeader 
  pageTitle="Cast Spotlights" 
  breadcrumbs={[{ label: "Cast Spotlights" }]}
/>

<!-- Introduction -->
<Section>
  <div class="max-w-4xl">
    <p class="text-lg text-gray-700 leading-relaxed mb-8">
      Meet the courageous individuals who shared their personal journeys of identity, acceptance, and love. 
      Each cast member offers a unique perspective on navigating sexuality and gender identity within 
      traditional South Asian families and communities.
    </p>
  </div>
</Section>

<!-- Cast Spotlights -->
<Section className="bg-gray-50">
  <div class="grid grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-8">
    {#each emergenceData.castSpotlights as spotlight}
      <div class="bg-white rounded-lg shadow-sm overflow-hidden">
        <VideoCard
          title="{spotlight.name}'s Story"
          runtime={spotlight.runtime}
          youtubeId={spotlight.youtubeId}
          description={spotlight.bio}
          className="border-0 shadow-none"
        />
        
        <div class="p-6 pt-0">
          <div class="flex justify-between items-center">
            <h3 class="text-xl font-semibold text-gray-900">{spotlight.name}</h3>
            <span class="text-sm text-gray-500">{spotlight.runtime}</span>
          </div>
          
          {#if spotlight.bio}
            <p class="text-gray-600 mt-3 leading-relaxed">
              {spotlight.bio}
            </p>
          {/if}
          
          <div class="mt-4 pt-4 border-t border-gray-200">
            <p class="text-xs text-gray-500">
              Individual cast spotlight featuring personal interviews and reflections
            </p>
          </div>
        </div>
      </div>
    {/each}
  </div>
</Section>

<!-- About the Cast -->
<Section title="About the Stories">
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">Individual Journeys</h3>
      <p class="text-gray-700 leading-relaxed">
        Each cast member brings their unique perspective to the documentary, sharing intimate details 
        about their experiences with family, community, and self-acceptance. These personal narratives 
        form the heart of the documentary's emotional impact.
      </p>
    </div>
    
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">Shared Experiences</h3>
      <p class="text-gray-700 leading-relaxed">
        While each story is unique, the cast members share common themes of courage, resilience, 
        and the complex navigation of identity within conservative cultural contexts. Their stories 
        provide hope and representation for others facing similar challenges.
      </p>
    </div>
  </div>
  
  <!-- Important Note -->
  <div class="mt-8 p-6 bg-amber-50 border border-amber-200 rounded-lg">
    <div class="flex">
      <div class="flex-shrink-0">
        <svg class="h-5 w-5 text-amber-400" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M8.485 2.495c.673-1.167 2.357-1.167 3.03 0l6.28 10.875c.673 1.167-.17 2.625-1.516 2.625H3.72c-1.347 0-2.189-1.458-1.515-2.625L8.485 2.495zM10 5a.75.75 0 01.75.75v3.5a.75.75 0 01-1.5 0v-3.5A.75.75 0 0110 5zm0 9a1 1 0 100-2 1 1 0 000 2z" clip-rule="evenodd"/>
        </svg>
      </div>
      <div class="ml-3">
        <h4 class="text-sm font-medium text-amber-800 mb-1">Privacy Notice</h4>
        <p class="text-sm text-amber-700">
          As per director requirements, Christine Michelle Lord's photo and biographical information 
          are excluded from this cast page in accordance with the official website guidelines.
        </p>
      </div>
    </div>
  </div>
</Section>

<!-- Related Links -->
<Section className="bg-emerald-50">
  <div class="text-center max-w-2xl mx-auto">
    <h3 class="text-xl font-semibold text-gray-900 mb-4">Explore More</h3>
    <p class="text-gray-700 mb-6">
      Learn more about the documentary and explore additional resources.
    </p>
    <div class="flex flex-col sm:flex-row gap-4 justify-center">
      <Button>
        <a href="/film" class="text-white no-underline">Watch the Full Film</a>
      </Button>
      <Button variant="outline">
        <a href="/stills" class="no-underline">Photo Gallery</a>
      </Button>
      <Button variant="outline">
        <a href={emergenceData.sources.officialSite} target="_blank" rel="noopener noreferrer" class="no-underline">
          Official Website
        </a>
      </Button>
    </div>
  </div>
</Section>

<SubFooter />