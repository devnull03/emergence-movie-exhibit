<script lang="ts">
  import { onMount, onDestroy } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger, ScrollSmoother, ScrollToPlugin } from "gsap/all";
  import emergenceData from "$lib/content/films/emergence.json";
  import { Header } from "@south-asian-canadian-digital-archive/sacda-exhibits-common";
  import SubHeader from "$lib/components/SubHeader.svelte";

  let smoother: globalThis.ScrollSmoother | undefined = $state();

  const scrollToMain = () => {
    gsap.to(window, {
      duration: 0.5,
      scrollTo: {
        y: "#main-content-start",
        autoKill: false,
      },
      ease: "power2.inOut",
    });
  };

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger, ScrollSmoother, ScrollToPlugin);

    // Create ScrollSmoother
    // smoother = ScrollSmoother.create({
    //   smooth: 1,
    //   effects: true,
    //   // smoothTouch: 0.1,
    //   normalizeScroll: true,
    // });

    ScrollTrigger.create({
      trigger: "#subheader",
      pin: true,
      start: "top",
      end: "max",
      pinType: "fixed",
      pinSpacing: false,
    });

    const isMobile = window.innerWidth < 768;

    let logoTl = gsap.timeline({
      scrollTrigger: {
        trigger: document.body,
        start: "top top",
        end: () => window.innerHeight * 0.25,
        scrub: 0.6,
      },
    });

    logoTl.fromTo(
      ".logo",
      {
        top: isMobile ? "50%" : "40vh",
        right: isMobile ? "50%" : "auto",
        xPercent: isMobile ? -50 : 0,
        yPercent: -50,
        scale: isMobile ? 0.8 : 1,
      },
      {
        top: isMobile ? "2rem" : "-14.5vh",
        right: isMobile ? "1rem" : "auto",
        xPercent: 0,
        yPercent: 0,
        scale: isMobile ? 0.15 : 0.15,
        duration: 0.1,
      }
    );

    const sections = gsap.utils.toArray("section");

    sections.forEach((panel, index) => {
      const lastIndex = sections.length - 1;

      switch (index) {
        case 0:
          ScrollTrigger.create({
            trigger: panel as Element,
            start: "top top",
            pin: !isMobile,
            pinSpacing: false,
          });
          break;

        case lastIndex:
          ScrollTrigger.create({
            trigger: panel as Element,
            start: "top top",
            end: isMobile ? "+=300px" : "+=615px",
            pin: true,
            pinSpacing: true,
          });
          break;

        default:
          ScrollTrigger.create({
            trigger: panel as Element,
            start: "top top",
            pin: !isMobile,
            pinSpacing: false,
          });
          break;
      }
    });
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

<div id="header-wrapper" class="relative z-100 overflow-x-hidden">
  <Header />
  <SubHeader />
</div>

<button
  type="button"
  class="logo h-[20vw] w-auto fixed z-150 border-none bg-transparent p-0 cursor-pointer"
  data-cursor-state="indicate-scroll-down"
  onclick={scrollToMain}
  aria-label="Scroll to main content"
>
  <img
    src="/src/lib/assets/logo.png"
    alt="Emergence: Out of the Shadows"
    class="relative top-0 left-0"
  />
</button>

<main>
  <div id="smooth-wrapper">
    <div id="smooth-content">
      <!-- Hero Section with Video Background -->
      <!-- svelte-ignore a11y_click_events_have_key_events -->
      <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
      <section
        class="relative w-full min-h-screen flex items-center justify-center bg-black overflow-hidden"
        data-cursor-state="indicate-scroll-down"
        aria-label="Click to scroll to main content"
        onclick={scrollToMain}
      >
        <!-- Background Video -->
        <video
          class="absolute inset-0 w-full h-full object-cover"
          autoplay
          muted
          loop
          playsinline
        >
          <source src="/src/lib/assets/trailer.mp4" type="video/mp4" />
          Your browser does not support the video tag.
        </video>

        <!-- Dark Overlay -->
        <div
          class="absolute inset-0 bg-black/50 flex justify-center items-center"
        ></div>
      </section>

      <!-- Content Sections -->
      <section
        id="main-content-start"
        class="relative w-full min-h-screen flex items-center justify-center bg-white"
      >
        <div class="max-w-4xl mx-auto px-8 text-center">
          <h2 class="text-5xl font-bold mb-8 text-gray-900">Cast Spotlights</h2>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            {#each emergenceData.castSpotlights || [] as cast}
              <div class="bg-gray-100 p-8 rounded-lg">
                <h3 class="text-2xl font-semibold mb-4">
                  {cast.name || "Unknown"}
                </h3>
                <p class="text-gray-600 mb-4">
                  {cast.bio || "No bio available"}
                </p>
                <p class="text-sm text-gray-500">
                  Runtime: {cast.runtime || "N/A"}
                </p>
              </div>
            {/each}
          </div>
        </div>
      </section>

      <section
        class="relative w-full min-h-screen flex items-center justify-center bg-gray-100"
      >
        <div class="max-w-4xl mx-auto px-8 text-center">
          <h2 class="text-5xl font-bold mb-8 text-gray-900">
            Awards & Recognition
          </h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div class="bg-white p-8 rounded-lg shadow-lg">
              <h3 class="text-3xl font-bold text-blue-600 mb-4">
                {emergenceData.awardsSummary?.countsByResult?.awardWinner ||
                  "0"}
              </h3>
              <p class="text-xl text-gray-700">Award Winner</p>
            </div>
            <div class="bg-white p-8 rounded-lg shadow-lg">
              <h3 class="text-3xl font-bold text-green-600 mb-4">
                {emergenceData.awardsSummary?.countsByResult
                  ?.totalOfficialSelections || "0"}
              </h3>
              <p class="text-xl text-gray-700">Official Selections</p>
            </div>
          </div>
        </div>
      </section>

      <section
        class="relative w-full min-h-screen flex items-center justify-center bg-gray-900 text-white"
      >
        <div class="max-w-4xl mx-auto px-8 text-center">
          <h2 class="text-5xl font-bold mb-8">Watch Now</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            {#each (emergenceData.versions || []).slice(0, 4) as version}
              <div class="bg-gray-800 p-8 rounded-lg">
                <h3 class="text-xl font-semibold mb-4">
                  {version.title || "Untitled"}
                </h3>
                <p class="text-gray-300 mb-4">
                  Runtime: {version.runtime || "N/A"}
                </p>
                <p class="text-sm text-gray-400">
                  Language: {version.lang || "N/A"}
                </p>
              </div>
            {/each}
          </div>
        </div>
      </section>

      <div class="h-[400px] md:h-[400px] sm:h-[800px]">
        <!-- footer spacing - more space needed on mobile -->
      </div>
    </div>
  </div>
</main>

<style>
  section {
    position: sticky;
    top: 0;
    width: 100%;
    min-height: 100vh;
  }
</style>
