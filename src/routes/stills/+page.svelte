<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
  import MetaHead from "$lib/components/MetaHead.svelte";
  import SubHeader from "$lib/components/SubHeader.svelte";
  import Section from "$lib/components/Section.svelte";
  import SubFooter from "$lib/components/SubFooter.svelte";
  import { Button } from "$lib/components/ui/button";
</script>

<MetaHead 
  title="Photo Gallery"
  description="Behind-the-scenes photos and promotional stills from Emergence: Out of the Shadows documentary"
  canonical="/stills"
/>

<SubHeader 
  pageTitle="Photo Gallery" 
  breadcrumbs={[{ label: "Photo Gallery" }]}
/>

<!-- Introduction -->
<Section>
  <div class="max-w-4xl">
    <p class="text-lg text-gray-700 leading-relaxed mb-8">
      Explore behind-the-scenes moments and promotional imagery from the making of 
      <em>{emergenceData.title}</em>. This collection captures the intimate nature 
      of the documentary and the powerful stories shared by our cast.
    </p>
  </div>
</Section>

<!-- Gallery Placeholder -->
<Section className="bg-gray-50">
  <div class="text-center py-16">
    <div class="max-w-md mx-auto">
      <div class="mb-6">
        <svg class="h-16 w-16 text-gray-400 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
        </svg>
      </div>
      
      <h3 class="text-xl font-semibold text-gray-900 mb-4">Gallery Coming Soon</h3>
      <p class="text-gray-600 mb-6">
        We're currently curating a collection of behind-the-scenes photos and promotional stills. 
        This gallery will feature intimate moments from production and key imagery from the documentary.
      </p>
      
      <div class="space-y-3 text-sm text-gray-500">
        <p>• Production photography</p>
        <p>• Cast portraits</p>
        <p>• Behind-the-scenes moments</p>
        <p>• Promotional materials</p>
      </div>
    </div>
  </div>
</Section>

<!-- Rights Information -->
<Section title="Usage Rights">
  <div class="bg-white rounded-lg border border-gray-200 p-6">
    <div class="flex">
      <div class="flex-shrink-0">
        <svg class="h-5 w-5 text-amber-400" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M8.485 2.495c.673-1.167 2.357-1.167 3.03 0l6.28 10.875c.673 1.167-.17 2.625-1.516 2.625H3.72c-1.347 0-2.189-1.458-1.515-2.625L8.485 2.495zM10 5a.75.75 0 01.75.75v3.5a.75.75 0 01-1.5 0v-3.5A.75.75 0 0110 5zm0 9a1 1 0 100-2 1 1 0 000 2z" clip-rule="evenodd"/>
        </svg>
      </div>
      <div class="ml-3">
        <h4 class="text-sm font-medium text-gray-800 mb-2">Important Copyright Notice</h4>
        <p class="text-sm text-gray-600 mb-3">
          All photographs and promotional materials are protected by copyright and are provided 
          for viewing purposes only. {emergenceData.rights.notice}
        </p>
        <p class="text-xs text-gray-500">
          For press inquiries, educational use, or licensing requests, please contact: 
          <a href="mailto:{emergenceData.rights.contactEmail}" class="text-emerald-600 hover:text-emerald-700">
            {emergenceData.rights.contactEmail}
          </a>
        </p>
      </div>
    </div>
  </div>
</Section>

<!-- Related Links -->
<Section className="bg-emerald-50">
  <div class="text-center max-w-2xl mx-auto">
    <h3 class="text-xl font-semibold text-gray-900 mb-4">Explore More Visual Content</h3>
    <p class="text-gray-700 mb-6">
      While you're waiting for the photo gallery, explore video content and learn more about the film.
    </p>
    <div class="flex flex-col sm:flex-row gap-4 justify-center">
      <Button>
        <a href="/film" class="text-white no-underline">Watch the Documentary</a>
      </Button>
      <Button variant="outline">
        <a href="/cast" class="no-underline">Cast Video Spotlights</a>
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