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
  title="Film"
  description={`Watch ${emergenceData.title} - ${emergenceData.synopsis}`}
  canonical="/film"
/>

<SubHeader 
  pageTitle="Film" 
  breadcrumbs={[{ label: "Film" }]}
/>

<!-- Film Overview -->
<Section title="About the Documentary">
  <div class="max-w-4xl">
    <p class="text-lg text-gray-700 leading-relaxed mb-6">
      {emergenceData.synopsis}
    </p>
    
    <div class="bg-emerald-50 rounded-lg p-6 mb-8">
      <h3 class="text-lg font-semibold text-emerald-900 mb-3">Educational Resource</h3>
      <p class="text-emerald-800 mb-4">
        A comprehensive teacher's discussion guide is available to support educational screenings and classroom discussions.
      </p>
      <Button variant="outline" class="border-emerald-600 text-emerald-700 hover:bg-emerald-100">
        <a href={emergenceData.teacherGuide.href} target="_blank" rel="noopener noreferrer" class="no-underline">
          {emergenceData.teacherGuide.title}
        </a>
      </Button>
    </div>
  </div>
</Section>

<!-- Film Versions -->
<Section title="Watch the Film" className="bg-gray-50">
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    {#each emergenceData.versions as version}
      <VideoCard
        title={version.title}
        runtime={version.runtime}
        youtubeId={version.id}
        description="Language: {version.lang === 'EN' ? 'English' : 
                     version.lang === 'FR' ? 'French' : 
                     version.lang === 'HI' ? 'Hindi' : 
                     version.lang === 'PA' ? 'Punjabi' : version.lang}"
      />
    {/each}
  </div>
  
  <div class="mt-8 p-6 bg-white rounded-lg border border-gray-200">
    <h3 class="text-lg font-semibold text-gray-900 mb-3">Viewing Options</h3>
    <ul class="text-gray-700 space-y-2">
      <li>• <strong>Broadcast Version (58 min):</strong> Television-length version suitable for broadcast</li>
      <li>• <strong>Full Documentary (81 min):</strong> Complete feature-length version</li>
      <li>• <strong>Multiple Languages:</strong> Available with English, French, Hindi, and Punjabi subtitles</li>
      <li>• <strong>Accessibility:</strong> All versions include closed captions</li>
    </ul>
  </div>
</Section>

<!-- Production Information -->
<Section title="Production Details">
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">Film Information</h3>
      <dl class="space-y-3 text-sm">
        <div class="flex justify-between">
          <dt class="font-medium text-gray-700">Runtime (Full):</dt>
          <dd class="text-gray-600">81 minutes</dd>
        </div>
        <div class="flex justify-between">
          <dt class="font-medium text-gray-700">Runtime (Broadcast):</dt>
          <dd class="text-gray-600">58 minutes</dd>
        </div>
        <div class="flex justify-between">
          <dt class="font-medium text-gray-700">Genre:</dt>
          <dd class="text-gray-600">Documentary</dd>
        </div>
        <div class="flex justify-between">
          <dt class="font-medium text-gray-700">Languages:</dt>
          <dd class="text-gray-600">English, French, Hindi, Punjabi</dd>
        </div>
        <div class="flex justify-between">
          <dt class="font-medium text-gray-700">Release:</dt>
          <dd class="text-gray-600">2021</dd>
        </div>
      </dl>
    </div>
    
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">Recognition</h3>
      <ul class="text-sm text-gray-700 space-y-2">
        <li>• {emergenceData.awardsSummary.countsByFestivalType.total} Official Festival Selections</li>
        <li>• {emergenceData.awardsSummary.countsByResult.awardWinner} Award Winners</li>
        <li>• {emergenceData.awardsSummary.countsByResult.finalist} Festival Finalists</li>
        <li>• Academy Award, BAFTA, and Canadian Screen Award Qualifying Festivals</li>
      </ul>
      
      <div class="mt-4">
        <Button variant="outline" size="sm">
          <a href="/awards" class="no-underline">View All Awards</a>
        </Button>
      </div>
    </div>
  </div>
</Section>

<!-- Links -->
<Section className="bg-emerald-50">
  <div class="text-center max-w-2xl mx-auto">
    <h3 class="text-xl font-semibold text-gray-900 mb-4">Learn More</h3>
    <p class="text-gray-700 mb-6">
      Explore cast spotlights, behind-the-scenes content, and additional resources.
    </p>
    <div class="flex flex-col sm:flex-row gap-4 justify-center">
      <Button>
        <a href="/cast" class="text-white no-underline">Cast Spotlights</a>
      </Button>
      <Button variant="outline">
        <a href="/stills" class="no-underline">Photo Gallery</a>
      </Button>
      <Button variant="outline">
        <a href="/sources" class="no-underline">Official Sources</a>
      </Button>
    </div>
  </div>
</Section>

<SubFooter />