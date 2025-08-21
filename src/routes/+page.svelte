<script lang="ts">
  import { onMount, onDestroy } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger, ScrollSmoother } from "gsap/all";
  import emergenceData from "$lib/content/films/emergence.json";
  import Section from "$lib/components/Section.svelte";
  import { Button } from "$lib/components/ui/button";
  import SubFooter from "$lib/components/SubFooter.svelte";

  let heroSection: HTMLElement;
  let heroTitle: HTMLElement;
  let backgroundVideo: HTMLVideoElement;
  let smoother: globalThis.ScrollSmoother | undefined = $state();

  onMount(() => {
    // Register GSAP plugins
    gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

    // Create ScrollSmoother
    smoother = ScrollSmoother.create({
      smooth: 2,
      effects: true,
      smoothTouch: true,
      normalizeScroll: true,
    });

    // Wait for elements to be available
    setTimeout(() => {
      if (heroTitle) {
        // Create GSAP timeline for hero title animation
        gsap
          .timeline({
            scrollTrigger: {
              trigger: heroSection,
              start: "top top",
              end: "bottom center",
              scrub: 1.5,
              pin: false,
            },
          })
          .to(heroTitle, {
            scale: 0.8,
            y: -100,
            opacity: 0.7,
            ease: "none",
          });
      }

      // Handle video optimization
      if (backgroundVideo) {
        const videoObserver = new IntersectionObserver(
          (entries) => {
            entries.forEach((entry) => {
              if (entry.isIntersecting) {
                backgroundVideo.play();
              } else {
                backgroundVideo.pause();
              }
            });
          },
          { threshold: 0.1 }
        );

        videoObserver.observe(backgroundVideo);
      }
    }, 100);
  });

  onDestroy(() => {
    smoother?.kill();
    ScrollTrigger.killAll();
  });
</script>

<svelte:head>
  <title>Emergence: Out of the Shadows - SACDA Digital Exhibit</title>
  <meta
    name="description"
    content="An intimate documentary following three South Asian LGBTQ+ individuals as they navigate identity, family, and belonging. Winner of 7 awards across 51 international film festivals."
  />
  <meta
    property="og:title"
    content="Emergence: Out of the Shadows - Digital Exhibit"
  />
  <meta
    property="og:description"
    content="Discover the powerful stories of Kayden, Jag, and Amar in this acclaimed documentary."
  />
</svelte:head>

<div id="smooth-content">
  <!-- Hero Section with Background Video -->
  <section
    bind:this={heroSection}
    data-speed="0.5"
    class="relative min-h-screen flex items-center justify-center overflow-hidden"
  >
    <!-- Background Video -->
    <video
      bind:this={backgroundVideo}
      class="absolute inset-0 w-full h-full object-cover z-0"
      autoplay
      muted
      loop
      playsinline
      preload="metadata"
    >
      <source src="/videos/emergence-background.webm" type="video/webm" />
      <source src="/videos/emergence-background.mp4" type="video/mp4" />
    </video>

    <!-- Dark overlay for better text readability -->
    <div class="absolute inset-0 bg-black/60 z-1"></div>

    <!-- Hero Content -->
    <div class="relative z-10 text-center text-white px-6 hero-title-container">
      <h1
        bind:this={heroTitle}
        class="text-6xl md:text-8xl lg:text-9xl font-bold mb-4 tracking-tight"
      >
        EMERGENCE
      </h1>
      <p class="text-xl md:text-2xl lg:text-3xl font-light opacity-90 mb-8">
        Out of the Shadows
      </p>
      <p
        class="text-lg md:text-xl text-gray-300 max-w-3xl mx-auto mb-12 leading-relaxed"
      >
        {emergenceData.synopsis}
      </p>
      <Button
        class="bg-emerald-600 hover:bg-emerald-700 text-white px-8 py-4 text-lg font-bold"
        onclick={() =>
          document
            .getElementById("story")
            ?.scrollIntoView({ behavior: "smooth" })}
      >
        Discover Their Stories →
      </Button>
    </div>
  </section>

  <!-- Story Section -->
  <div id="story" data-speed="0.8" class="parallax-section">
    <Section title="The Story" className="bg-white">
      <div class="max-w-4xl mx-auto">
        <p class="text-xl leading-relaxed mb-8 text-gray-700">
          {emergenceData.synopsis}
        </p>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-12 mb-12">
          <div>
            <h3 class="text-2xl font-bold mb-6 text-emerald-600">
              Available Versions
            </h3>
            <ul class="space-y-3">
              {#each emergenceData.versions as version}
                <li class="flex items-start">
                  <span class="text-emerald-500 mr-3 text-xl">•</span>
                  <div>
                    <span class="text-lg text-gray-700 font-semibold"
                      >{version.title}</span
                    >
                    <div class="text-sm text-gray-600">
                      Runtime: {version.runtime}
                    </div>
                  </div>
                </li>
              {/each}
            </ul>
          </div>

          <div>
            <h3 class="text-2xl font-bold mb-6 text-emerald-600">
              Festival Recognition
            </h3>
            <div class="space-y-4">
              <div class="flex justify-between border-b pb-2">
                <span class="text-gray-600">Total Festivals:</span>
                <span class="font-semibold"
                  >{emergenceData.awardsSummary.countsByResult
                    .totalOfficialSelections}</span
                >
              </div>
              <div class="flex justify-between border-b pb-2">
                <span class="text-gray-600">Awards Won:</span>
                <span class="font-semibold"
                  >{emergenceData.awardsSummary.countsByResult
                    .awardWinner}</span
                >
              </div>
              <div class="flex justify-between border-b pb-2">
                <span class="text-gray-600">Finalist:</span>
                <span class="font-semibold"
                  >{emergenceData.awardsSummary.countsByResult.finalist}</span
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </Section>
  </div>

  <!-- Trailer Section -->
  <div id="trailer" data-speed="0.9" class="parallax-section">
    <Section title="Watch Trailer" className="bg-black text-white">
      <div class="max-w-4xl mx-auto">
        <div class="aspect-video rounded-lg overflow-hidden mb-8">
          <iframe
            src="https://www.youtube.com/embed/{emergenceData.trailer
              .youtubeId}"
            title="Emergence: Out of the Shadows - Official Trailer"
            class="w-full h-full"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </div>

        <div class="text-center">
          <p class="text-lg text-gray-300 mb-6">
            Experience the powerful trailer that has captivated audiences at
            film festivals worldwide
          </p>
          <Button
            variant="outline"
            class="border-2 border-white text-white hover:bg-white hover:text-black px-8 py-3 text-lg font-bold"
            onclick={() =>
              window.open(
                `https://www.youtube.com/watch?v=${emergenceData.trailer.youtubeId}`,
                "_blank"
              )}
          >
            Watch on YouTube →
          </Button>
        </div>
      </div>
    </Section>
  </div>

  <!-- Watch Section -->
  <div id="watch" data-speed="0.7" class="parallax-section">
    <Section title="Watch the Film" className="bg-gray-50">
      <div class="max-w-6xl mx-auto">
        <div class="text-center mb-12">
          <p class="text-xl text-gray-700 mb-8">
            Ready to watch the full documentary? Choose your preferred version
            below.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          {#each emergenceData.versions as version}
            <div
              class="bg-white rounded-lg shadow-lg p-6 text-center border-2 border-transparent hover:border-emerald-500 transition-colors"
            >
              <div class="text-4xl mb-4">🎬</div>
              <h3 class="text-xl font-bold mb-2">{version.title}</h3>
              <p class="text-gray-600 mb-4">Language: {version.lang}</p>
              <div class="text-2xl font-bold text-emerald-600 mb-4">
                {version.runtime}
              </div>
              <Button
                class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold"
                onclick={() =>
                  window.open(
                    `https://www.youtube.com/watch?v=${version.id}`,
                    "_blank"
                  )}
              >
                Watch Now →
              </Button>
            </div>
          {/each}
        </div>

        <!-- Educational Resources -->
        <div class="mt-16 bg-emerald-600 rounded-lg p-8 text-white text-center">
          <h3 class="text-2xl font-bold mb-4">For Educators</h3>
          <p class="text-emerald-100 mb-6 text-lg">
            Download our comprehensive teacher's discussion guide for classroom
            use
          </p>
          <Button
            variant="outline"
            class="border-2 border-white text-white hover:bg-white hover:text-emerald-600 px-8 py-3 text-lg font-bold"
            onclick={() =>
              window.open(emergenceData.teacherGuide.href, "_blank")}
          >
            {emergenceData.teacherGuide.title} →
          </Button>
        </div>
      </div>
    </Section>
  </div>

  <!-- Cast Spotlights Section -->
  <div id="cast" data-speed="0.6" class="parallax-section">
    <Section title="Cast Spotlights" className="bg-black text-white">
      <div class="max-w-6xl mx-auto">
        <p class="text-lg text-center mb-12 text-gray-300">
          Personal stories from our three protagonists
        </p>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          {#each emergenceData.castSpotlights as cast}
            <div
              class="bg-gray-900 rounded-lg overflow-hidden border border-gray-800"
            >
              <div class="aspect-video overflow-hidden">
                <iframe
                  src="https://www.youtube.com/embed/{cast.youtubeId}"
                  title="{cast.name} - Character Spotlight"
                  class="w-full h-full"
                  frameborder="0"
                  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                  allowfullscreen
                  loading="lazy"
                ></iframe>
              </div>
              <div class="p-6">
                <h3 class="text-xl font-bold mb-2 text-emerald-400">
                  {cast.name}
                </h3>
                <p class="text-gray-300 mb-4">{cast.bio}</p>
                <div class="text-sm text-gray-400">Runtime: {cast.runtime}</div>
              </div>
            </div>
          {/each}
        </div>
      </div>
    </Section>
  </div>

  <!-- Awards Section -->
  <div id="awards" data-speed="0.8" class="parallax-section">
    <Section title="Recognition & Awards" className="bg-white">
      <div class="max-w-6xl mx-auto">
        <!-- Award Statistics -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mb-12">
          <div
            class="text-center p-6 border border-emerald-200 rounded-lg bg-emerald-50"
          >
            <div class="text-4xl font-bold text-emerald-600 mb-2">
              {emergenceData.awardsSummary.countsByResult
                .totalOfficialSelections}
            </div>
            <div class="text-sm text-gray-600 uppercase tracking-wide">
              Festival Selections
            </div>
          </div>
          <div
            class="text-center p-6 border border-emerald-200 rounded-lg bg-emerald-50"
          >
            <div class="text-4xl font-bold text-emerald-600 mb-2">
              {emergenceData.awardsSummary.countsByResult.awardWinner}
            </div>
            <div class="text-sm text-gray-600 uppercase tracking-wide">
              Award Wins
            </div>
          </div>
          <div
            class="text-center p-6 border border-emerald-200 rounded-lg bg-emerald-50"
          >
            <div class="text-4xl font-bold text-emerald-600 mb-2">
              {emergenceData.awardsSummary.countsByResult.finalist}
            </div>
            <div class="text-sm text-gray-600 uppercase tracking-wide">
              Finalist
            </div>
          </div>
          <div
            class="text-center p-6 border border-emerald-200 rounded-lg bg-emerald-50"
          >
            <div class="text-4xl font-bold text-emerald-600 mb-2">
              {emergenceData.awardsSummary.countsByResult.semiFinalist}
            </div>
            <div class="text-sm text-gray-600 uppercase tracking-wide">
              Semi-Finalist
            </div>
          </div>
        </div>

        <div class="mb-12">
          <h3 class="text-2xl font-bold mb-8 text-center text-emerald-600">
            Major Awards
          </h3>
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            {#each emergenceData.awardsHighlights.slice(0, 6) as award}
              <div
                class="bg-gray-50 rounded-lg p-6 border-l-4 border-emerald-500"
              >
                <h4 class="font-bold text-emerald-600 mb-2">{award.result}</h4>
                <p class="text-gray-800 font-semibold mb-1">{award.festival}</p>
                <p class="text-gray-600 text-sm">{award.title}</p>
              </div>
            {/each}
          </div>
        </div>
      </div>
    </Section>
  </div>

  <!-- Contact & Rights Section -->
  <div id="contact" data-speed="0.9" class="parallax-section">
    <Section title="Contact & Rights" className="bg-gray-900 text-white">
      <div class="max-w-6xl mx-auto">
        <!-- Usage Notice -->
        <div class="bg-amber-500 text-black rounded-lg p-6 mb-12">
          <h3 class="text-lg font-bold mb-2 flex items-center">
            <span class="mr-2">⚠</span> IMPORTANT USAGE NOTICE
          </h3>
          <p class="font-semibold">
            {emergenceData.rights.notice}
          </p>
        </div>

        <!-- Contact Information -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12 mb-12">
          <div>
            <h3 class="text-2xl font-bold mb-6 text-emerald-400">
              Primary Contact
            </h3>
            <div class="bg-gray-800 rounded-lg p-6 border border-gray-700">
              <div class="flex items-center mb-4">
                <span class="text-3xl mr-4">📧</span>
                <div>
                  <div class="text-xl font-bold">
                    Film Rights & Distribution
                  </div>
                  <div class="text-gray-400">
                    For all screening and licensing inquiries
                  </div>
                </div>
              </div>
              <div class="text-center py-4">
                <a
                  href="mailto:{emergenceData.rights.contactEmail}"
                  class="text-2xl font-bold text-emerald-400 hover:text-emerald-300 transition-colors"
                >
                  {emergenceData.rights.contactEmail}
                </a>
              </div>
              <div class="flex gap-4 justify-center mt-6">
                <Button
                  class="bg-emerald-600 hover:bg-emerald-700"
                  onclick={() =>
                    window.open(
                      `mailto:${emergenceData.rights.contactEmail}`,
                      "_blank"
                    )}
                >
                  Send General Inquiry
                </Button>
              </div>
            </div>
          </div>

          <div>
            <h3 class="text-2xl font-bold mb-6 text-emerald-400">
              Contact Information
            </h3>
            <div class="bg-gray-800 rounded-lg p-6 border border-gray-700">
              <div class="space-y-4">
                <div class="flex items-start gap-4">
                  <div class="flex-shrink-0">
                    <span class="text-3xl">📧</span>
                  </div>
                  <div class="flex-1">
                    <div class="text-lg font-bold text-white">
                      Film Rights & Distribution
                    </div>
                    <div class="text-emerald-400 text-sm mb-2">
                      For all screening and licensing inquiries
                    </div>
                    <a
                      href="mailto:{emergenceData.rights.contactEmail}"
                      class="text-emerald-400 hover:text-emerald-300 transition-colors"
                    >
                      {emergenceData.rights.contactEmail}
                    </a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Usage Categories -->
        <div>
          <h3 class="text-2xl font-bold mb-8 text-center text-emerald-400">
            Usage Categories
          </h3>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <div
              class="bg-gray-800 rounded-lg p-6 border border-gray-700 text-center"
            >
              <div class="text-4xl mb-4">🎓</div>
              <h4 class="text-xl font-bold text-white mb-4">Educational Use</h4>
              <ul class="text-gray-300 text-left space-y-2">
                <li>• Classroom screenings</li>
                <li>• Academic workshops</li>
                <li>• Student research</li>
                <li>• Discussion groups</li>
              </ul>
            </div>
            <div
              class="bg-gray-800 rounded-lg p-6 border border-gray-700 text-center"
            >
              <div class="text-4xl mb-4">📺</div>
              <h4 class="text-xl font-bold text-white mb-4">Press & Media</h4>
              <ul class="text-gray-300 text-left space-y-2">
                <li>• Press coverage</li>
                <li>• Interview requests</li>
                <li>• Promotional materials</li>
                <li>• Festival submissions</li>
              </ul>
            </div>
            <div
              class="bg-gray-800 rounded-lg p-6 border border-gray-700 text-center"
            >
              <div class="text-4xl mb-4">👥</div>
              <h4 class="text-xl font-bold text-white mb-4">Community</h4>
              <ul class="text-gray-300 text-left space-y-2">
                <li>• Non-profit events</li>
                <li>• Community centers</li>
                <li>• Awareness campaigns</li>
                <li>• Support groups</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </Section>
  </div>

  <!-- SubFooter Component -->
</div>

<style>
  #smooth-content {
    overflow: visible;
    width: 100%;
  }

  .hero-title-container {
    transform-origin: center center;
    will-change: transform;
  }

  /* Optimized video performance */
  video {
    will-change: transform;
    transform: translate3d(0, 0, 0); /* Force hardware acceleration */
  }

  /* Parallax sections */
  .parallax-section {
    will-change: transform;
  }

  /* Smooth transitions for GSAP animations */
  .hero-title-container h1 {
    will-change: transform;
  }
</style>
