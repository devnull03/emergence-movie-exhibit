<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
  import MetaHead from "$lib/components/MetaHead.svelte";
  import Section from "$lib/components/Section.svelte";
  import VideoCard from "$lib/components/VideoCard.svelte";
  import SubFooter from "$lib/components/SubFooter.svelte";
  import Alert from "$lib/components/Alert.svelte";
  import { Button } from "$lib/components/ui/button";
</script>

<MetaHead 
  title="Home"
  description={emergenceData.synopsis}
  canonical="/"
/>

<!-- Rights Alert -->
<Alert 
  type="warning" 
  message={emergenceData.rights.notice}
  className="mx-6 mt-6"
/>

<!-- Hero Section -->
<Section className="text-center bg-gradient-to-b from-gray-50 to-white">
  <div class="max-w-4xl mx-auto">
    <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-gray-900 mb-6 leading-tight">
      {emergenceData.title}
    </h1>
    
    <p class="text-xl text-gray-700 mb-8 leading-relaxed">
      {emergenceData.synopsis}
    </p>
    
    <!-- Trailer -->
    <div class="max-w-2xl mx-auto mb-8">
      <VideoCard
        title="Official Trailer"
        youtubeId={emergenceData.trailer.youtubeId}
      />
    </div>
    
    <!-- CTA Buttons -->
    <div class="flex flex-col sm:flex-row gap-4 justify-center">
      <Button size="lg" class="bg-emerald-600 hover:bg-emerald-700">
        <a href="/film" class="text-white no-underline">Watch the Film</a>
      </Button>
      <Button variant="outline" size="lg">
        <a href="/cast" class="no-underline">Meet the Cast</a>
      </Button>
      <Button variant="outline" size="lg">
        <a href="/awards" class="no-underline">Awards & Recognition</a>
      </Button>
    </div>
  </div>
</Section>

<!-- Quick Stats -->
<Section className="bg-emerald-50">
  <div class="grid grid-cols-1 md:grid-cols-3 gap-8 text-center">
    <div>
      <div class="text-4xl font-bold text-emerald-600 mb-2">
        {emergenceData.awardsSummary.countsByFestivalType.total}
      </div>
      <div class="text-gray-700 font-medium">Official Selections</div>
    </div>
    <div>
      <div class="text-4xl font-bold text-emerald-600 mb-2">
        {emergenceData.awardsSummary.countsByResult.awardWinner}
      </div>
      <div class="text-gray-700 font-medium">Award Winners</div>
    </div>
    <div>
      <div class="text-4xl font-bold text-emerald-600 mb-2">
        {emergenceData.versions.length}
      </div>
      <div class="text-gray-700 font-medium">Language Versions</div>
    </div>
  </div>
</Section>

<!-- Key Links -->
<Section title="Explore">
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    <div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6">
      <h3 class="text-xl font-semibold text-gray-900 mb-3">Watch the Film</h3>
      <p class="text-gray-600 mb-4">Available in multiple languages with subtitles</p>
      <Button variant="outline" size="sm">
        <a href="/film" class="no-underline">View Versions</a>
      </Button>
    </div>
    
    <div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6">
      <h3 class="text-xl font-semibold text-gray-900 mb-3">Cast Spotlights</h3>
      <p class="text-gray-600 mb-4">Personal stories from Amar, Jag, and Kayden</p>
      <Button variant="outline" size="sm">
        <a href="/cast" class="no-underline">Meet the Cast</a>
      </Button>
    </div>
    
    <div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6">
      <h3 class="text-xl font-semibold text-gray-900 mb-3">Awards & Festivals</h3>
      <p class="text-gray-600 mb-4">51 official selections and multiple awards</p>
      <Button variant="outline" size="sm">
        <a href="/awards" class="no-underline">View Recognition</a>
      </Button>
    </div>
    
    <div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6">
      <h3 class="text-xl font-semibold text-gray-900 mb-3">Educational Resources</h3>
      <p class="text-gray-600 mb-4">Teacher's discussion guide available</p>
      <Button variant="outline" size="sm">
        <a href={emergenceData.teacherGuide.href} target="_blank" rel="noopener noreferrer" class="no-underline">
          Download Guide
        </a>
      </Button>
    </div>
    
    <div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6">
      <h3 class="text-xl font-semibold text-gray-900 mb-3">Photo Gallery</h3>
      <p class="text-gray-600 mb-4">Behind the scenes and promotional stills</p>
      <Button variant="outline" size="sm">
        <a href="/stills" class="no-underline">View Gallery</a>
      </Button>
    </div>
    
    <div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6">
      <h3 class="text-xl font-semibold text-gray-900 mb-3">Learn More</h3>
      <p class="text-gray-600 mb-4">Official website and archive resources</p>
      <Button variant="outline" size="sm">
        <a href="/sources" class="no-underline">View Sources</a>
      </Button>
    </div>
  </div>
</Section>

<SubFooter />
