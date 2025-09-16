<script lang="ts">
  import SectionTitle from "../SectionTitle.svelte";
  import Section from "../Section.svelte";
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
  class="w-full h-screen flex flex-col items-center justify-center gap-8 px-8 font-[Poppins] tracking-tight leading-relaxed bg-background"
>
  <SectionTitle title="Synopsis" color="text-gray-900" />

  <div class="max-w-4xl mx-auto text-center space-y-8">
    <!-- Logline -->
    <div class="">
      <!-- <h3 class="mb-2">Logline</h3> -->
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
        <button class="px-4 py-2 underline italic text-xs underline-offset-2 cursor-pointer" onclick={() => selectLanguage(langCode)}>
          {langData.name}
        </button>
      {/each}
    </div>
  </div>
</Section>
