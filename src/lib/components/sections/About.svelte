<script lang="ts">
  import SectionTitle from "../SectionTitle.svelte";
  import Section from "../Section.svelte";
  import { Button } from "../ui/button";
  import synopsisData from "../../content/synopsis.json";

  let selectedLanguage = $state("en");

  let currentSynopsis = $derived.by(() => {
    const lang =
      synopsisData.languages[
        selectedLanguage as keyof typeof synopsisData.languages
      ];
    if (!lang || !lang.synopsis) return synopsisData.languages.en.synopsis;
    return lang.synopsis;
  });

  let currentLogline = $derived.by(() => {
    const lang =
      synopsisData.languages[
        selectedLanguage as keyof typeof synopsisData.languages
      ];
    if (!lang || !lang.synopsis || !("logline" in lang.synopsis)) {
      return synopsisData.languages.en.synopsis.logline;
    }
    return lang.synopsis.logline;
  });

  let currentLongSynopsis = $derived.by(() => {
    const lang =
      synopsisData.languages[
        selectedLanguage as keyof typeof synopsisData.languages
      ];
    if (!lang || !lang.synopsis || !("long" in lang.synopsis)) {
      return synopsisData.languages.en.synopsis.long;
    }
    return lang.synopsis.long;
  });

  let availableLanguages = $derived(Object.entries(synopsisData.languages));

  function selectLanguage(langCode: string) {
    selectedLanguage = langCode;
  }
</script>

<Section
  class="w-full h-screen flex flex-col items-center justify-center gap-8 font-[Poppins] tracking-tight leading-relaxed bg-background"
>
  <SectionTitle title="Synopsis" color="text-gray-900" />

  <div class="text-center space-y-8 max-w-prose mx-auto">
    <!-- Logline -->
    <div class="">
      <div class="text-lg leading-tight">
        {currentLogline}
      </div>
    </div>

    <!-- Long Synopsis -->
    <div class="">
      <h3 class="mb-2 italic text-xl">Synopsis</h3>
      <div class="text-sm leading-relaxed">
        {currentLongSynopsis}
      </div>
    </div>

    <!-- Language selector buttons -->
    <div class="flex flex-wrap justify-center gap-3 mt-8">
      {#each availableLanguages as [langCode, langData]}
        <button
          class="px-4 py-2 underline italic text-xs underline-offset-2 cursor-pointer"
          onclick={() => selectLanguage(langCode)}
        >
          {langData.name}
        </button>
      {/each}
    </div>

    <!-- Additional Information -->
    <div class="border-t border-gray-200 pt-6 space-y-6">
      <!-- Quick Actions -->
      <div class="flex flex-wrap justify-center gap-4">
        <Button
          href="https://emergencefilm.net/"
          target="_blank"
          rel="noopener noreferrer"
          variant="outline"
          size="sm"
          class="text-xs"
        >
          Official Website
        </Button>
        <Button
          href="https://emergencefilm.net/videos/"
          target="_blank"
          rel="noopener noreferrer"
          variant="outline"
          size="sm"
          class="text-xs"
        >
          Watch Trailer
        </Button>
        <Button
          href="https://emergencefilm.net/download-discussion-guide/"
          target="_blank"
          rel="noopener noreferrer"
          variant="outline"
          size="sm"
          class="text-xs"
        >
          Discussion Guide
        </Button>
      </div>

      <!-- Acknowledgment -->
      <div class="bg-gray-50 rounded-lg p-4 text-xs leading-relaxed space-y-2">
        <p class="font-medium text-gray-700">Acknowledgment</p>
        <p class="text-gray-600">
          This digital showcase was created with the generous permission and
          support of Sher Films and the production team behind <em
            >Emergence: Out of the Shadows</em
          >. We extend our gratitude to Producer Alex Sangha, Director Vinay
          Giridhar, and the entire cast and crew for sharing their powerful
          story with the world.
        </p>
        <p class="text-gray-600">
          For more information about the film, screenings, and educational
          resources, please visit
          <a
            href="https://emergencefilm.net/"
            target="_blank"
            rel="noopener noreferrer"
            class="text-primary hover:underline font-medium"
          >
            emergencefilm.net
          </a>
        </p>
      </div>

      <!-- Social Links -->
      <div class="flex justify-center gap-4 text-xs">
        <a
          href="https://www.instagram.com/emergencefilm/"
          target="_blank"
          rel="noopener noreferrer"
          class="text-gray-500 hover:text-gray-700 underline underline-offset-2"
        >
          Instagram
        </a>
        <a
          href="https://www.facebook.com/emergencefilm/"
          target="_blank"
          rel="noopener noreferrer"
          class="text-gray-500 hover:text-gray-700 underline underline-offset-2"
        >
          Facebook
        </a>
        <a
          href="https://twitter.com/Emergence_film"
          target="_blank"
          rel="noopener noreferrer"
          class="text-gray-500 hover:text-gray-700 underline underline-offset-2"
        >
          Twitter
        </a>
      </div>
    </div>
  </div>
</Section>
