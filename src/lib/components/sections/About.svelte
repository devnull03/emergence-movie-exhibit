<script lang="ts">
  import SectionTitle from "../SectionTitle.svelte";
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

<section
  class="w-full h-screen text-black flex flex-col items-center justify-center gap-8 px-8"
>
  <SectionTitle title="Synopsis" color="text-black" />

  <div class="max-w-4xl mx-auto text-center space-y-8">
    <!-- Logline -->
    <div class="border-l-4 border-black pl-6">
      <h3
        class="text-sm font-semibold text-gray-600 uppercase tracking-wide mb-2"
      >
        Logline
      </h3>
      <div class="text-xl font-medium leading-relaxed text-gray-900 italic">
        {currentLogline}
      </div>
    </div>

    <!-- Long Synopsis -->
    <div class="border-l-4 border-gray-300 pl-6">
      <h3
        class="text-sm font-semibold text-gray-600 uppercase tracking-wide mb-2"
      >
        Synopsis
      </h3>
      <div class="text-lg leading-relaxed text-gray-800">
        {currentLongSynopsis}
      </div>
    </div>

    <!-- Language selector buttons -->
    <div class="flex flex-wrap justify-center gap-3 mt-8">
      {#each availableLanguages as [langCode, langData]}
        <button
          class="px-4 py-2 rounded-lg text-sm font-medium transition-all duration-200
                 {selectedLanguage === langCode
            ? 'bg-black text-white shadow-lg'
            : 'bg-gray-100 text-gray-700 hover:bg-gray-200'}"
          onclick={() => selectLanguage(langCode)}
        >
          {langData.name}
        </button>
      {/each}
    </div>
  </div>
</section>
