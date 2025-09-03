<script lang="ts">
  import { onMount, onDestroy } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger, ScrollSmoother, ScrollToPlugin } from "gsap/all";
  import emergenceData from "$lib/content/films/emergence.json";

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

    // Create ScrollSmoother for smoother scrolling
    // smoother = ScrollSmoother.create({
    //   smooth: 1.2,
    //   effects: true,
    //   smoothTouch: 0.1,
    //   normalizeScroll: true,
    // });

    // const isMobile = window.innerWidth < 768;
    // const sections = gsap.utils.toArray("section");

    // sections.forEach((panel, index) => {
    //   const isLastSection = index === sections.length - 1;

    //   if (isLastSection) {
    //     // Last section needs special handling for footer spacing
    //     ScrollTrigger.create({
    //       trigger: panel as Element,
    //       start: "top top",
    //       end: isMobile ? "+=300px" : "+=615px",
    //       // pin: true,
    //       // pinSpacing: true,
    //     });
    //   } else {
    //     // All other sections use consistent pinning
    //     ScrollTrigger.create({
    //       trigger: panel as Element,
    //       start: "top top",
    //       end: "bottom top",
    //       // pin: true,
    //       // pinSpacing: false,
    //     });
    //   }
    // });

    // // Refresh ScrollTrigger after a short delay to ensure proper calculation
    // setTimeout(() => {
    //   ScrollTrigger.refresh();
    // }, 100);
  });

  onDestroy(() => {
    // smoother?.kill();
    // ScrollTrigger.killAll();
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

<main>
  <div id="smooth-wrapper">
    <div id="smooth-content">
      <!-- svelte-ignore a11y_click_events_have_key_events -->
      <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
      <section
        class="relative w-full min-h-screen flex items-center justify-center overflow-hidden"
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

        <!-- Dark Overlay  box-border shadow-[inset_0_0_10px_10px_black] -->
        <div
          class="absolute inset-0 flex justify-center items-center"
        ></div>

        <div class="relative z-10 text-center px-4 w-[80vw] overflow-x-hidden">
          <img
            src="/src/lib/assets/logo.png"
            alt="Emergence: Out of the Shadows"
            class=""
          />
        </div>
      </section>

      <!-- Content Sections -->
      <section
        id="main-content-start"
        class="w-full min-h-screen flex items-center justify-center bg-black"
      >
        <div class="text-white text-3xl font-bold">
          [Placeholder: Cast Spotlights]
        </div>
      </section>

      <section
        class="w-full min-h-screen flex items-center justify-center bg-gray-100"
      >
        <div class="text-gray-900 text-3xl font-bold">
          [Placeholder: Awards & Recognition]
        </div>
      </section>

      <section
        class="w-full min-h-screen flex items-center justify-center bg-gray-900 text-white"
      >
        <div class="text-white text-3xl font-bold">
          [Placeholder: Watch Now]
        </div>
      </section>
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
