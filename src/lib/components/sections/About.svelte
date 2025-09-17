<script lang="ts">
  import SectionTitle from "../SectionTitle.svelte";
  import Section from "../Section.svelte";
  import { Button } from "../ui/button";
  import synopsisData from "../../content/synopsis.json";
  import logo from "$lib/assets/logo.png";
  import Instagram from "$lib/icons/Instagram.svelte";

  import { ExternalLink, Facebook, Twitter } from "@lucide/svelte";

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
  class="w-full h-screen flex *:flex *:flex-col items-center justify-center *:gap-4 text-justify font-[Poppins] tracking-tight leading-relaxed bg-background"
>
  <SectionTitle title="Synopsis" color="text-gray-900" />

  <div class="flex items-start max-w-4xl mx-auto">
    <div class="flex-shrink-0">
      <img src={logo} alt="Emergence: Out of the Shadows" class="w-[30vw]" />
    </div>

    <div class="flex-1 space-y-4">
      <div class="space-y-2">
        <h3 class="text-lg font-semibold text-gray-900">
          Emergence: Out of the Shadows
        </h3>
        <p class="text-sm text-gray-600">
          A powerful documentary exploring LGBTQ+ stories in South Asian
          communities
        </p>
      </div>

      <!-- Quick Links -->
      <div class="flex gap-4">
        <a
          href="https://emergencefilm.net/"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center gap-2 text-xs text-gray-600 hover:text-gray-900 transition-colors"
        >
          <ExternalLink class="w-4 h-4" />
          Official Website
        </a>
        <a
          href="https://emergencefilm.net/videos/"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center gap-2 text-xs text-gray-600 hover:text-gray-900 transition-colors"
        >
          <ExternalLink class="w-4 h-4" />
          Watch Trailer
        </a>
        <a
          href="https://emergencefilm.net/download-discussion-guide/"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center gap-2 text-xs text-gray-600 hover:text-gray-900 transition-colors"
        >
          <ExternalLink class="w-4 h-4" />
          Discussion Guide
        </a>
      </div>

      <!-- Social Links -->
      <div class="flex gap-4">
        <a
          href="https://www.instagram.com/emergencefilm/"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center gap-2 text-xs text-gray-600 hover:text-gray-900 transition-colors"
        >
          <Instagram class="w-4 h-4" />
          Instagram
        </a>
        <a
          href="https://www.facebook.com/emergencefilm/"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center gap-2 text-xs text-gray-600 hover:text-gray-900 transition-colors"
        >
          <Facebook class="w-4 h-4" />
          Facebook
        </a>
        <a
          href="https://twitter.com/Emergence_film"
          target="_blank"
          rel="noopener noreferrer"
          class="flex items-center gap-2 text-xs text-gray-600 hover:text-gray-900 transition-colors"
        >
          <Twitter class="w-4 h-4" />
          Twitter
        </a>
      </div>
    </div>
  </div>

  <!-- Divider -->
  <div class="w-full max-w-3xl mx-auto pb-2 border-t border-gray-400"></div>

  <!-- <div class="text-center space-y-8 mx-auto"> -->
  <!-- Logline -->
  <div class="max-w-4xl mx-auto">
    <div class="text-lg leading-tight">
      {currentLogline}
    </div>
  </div>

  <!-- Long Synopsis -->
  <div class="max-w-4xl mx-auto">
    <h3 class="mb-2 italic text-xl text-center">Synopsis</h3>
    <div class="text-sm leading-relaxed">
      {currentLongSynopsis}
    </div>
  </div>

  <!-- Language selector buttons -->
  <div class="flex flex-wrap justify-center gap-3">
    {#each availableLanguages as [langCode, langData]}
      <button
        class="px-4 py-2 underline italic text-xs underline-offset-2 cursor-pointer"
        onclick={() => selectLanguage(langCode)}
      >
        {langData.name}
      </button>
    {/each}
  </div>

  <!-- </div> -->
</Section>
