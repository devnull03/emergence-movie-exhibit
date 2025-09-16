<script lang="ts">
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger, ScrollToPlugin } from "gsap/all";
  import CastSection from "$lib/components/sections/CastSection.svelte";
  import About from "$lib/components/sections/About.svelte";
  import trailer from "$lib/assets/trailer.mp4";
  import { asset } from "$app/paths";
  import Awards from "$lib/components/sections/Awards.svelte";
  import WatchNow from "$lib/components/sections/WatchNow.svelte";
  import emergence from "$lib/content/emergence.json";

  let awardsSection: HTMLElement;
  let awardsComponent: Awards;

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
    gsap.registerPlugin(ScrollTrigger, ScrollToPlugin);

    // apply parallax effect to any element with a data-speed attribute
    gsap.to("[data-speed]", {
      y: (i, el) =>
        (1 - parseFloat(el.getAttribute("data-speed"))) *
        ScrollTrigger.maxScroll(window),
      ease: "none",
      scrollTrigger: {
        start: 0,
        end: "max",
        invalidateOnRefresh: true,
        scrub: 0,
      },
    });

    // Awards section pinning
    if (awardsSection) {
      const awards = emergence.awardsHighlights;

      const pinTrigger = ScrollTrigger.create({
        trigger: awardsSection,
        start: "top top",
        end: () => `+=${awards.length * 100}vh`,
        pin: true,
        pinSpacing: true,
        scrub: 1,
        // markers: true,
        onUpdate: (self) => {
          const progress = Math.min(self.progress, 0.99);
          const newIndex = Math.floor(progress * awards.length);
          console.log(
            "Main page ScrollTrigger - progress:",
            self.progress,
            "newIndex:",
            newIndex
          );

          // Update award index
          if (awardsComponent && awardsComponent.updateAwardIndex) {
            awardsComponent.updateAwardIndex(newIndex);
          }

          // Update scroll progress for image parallax
          if (awardsComponent && awardsComponent.updateScrollProgress) {
            awardsComponent.updateScrollProgress(self.progress);
          }
        },
      });

      console.log("Awards ScrollTrigger created:", pinTrigger);
    }
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

<main class="*:rounded-t-2xl">
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
  <section
    class="relative w-full min-h-screen flex items-center justify-center overflow-hidden rounded-none! *:rounded-none!"
    data-cursor-state="indicate-scroll-down"
    aria-label="Click to scroll to main content"
    onclick={scrollToMain}
  >
    <!-- Background Video -->
    <video
      class="absolute inset-0 w-full h-full object-cover pointer-events-none"
      autoplay
      muted
      loop
      playsinline
      disablePictureInPicture={true}
      controls={false}
    >
      <source src={trailer} type="video/mp4" />
      Your browser does not support the video tag.
    </video>

    <!-- Dark Overlay  box-border shadow-[inset_0_0_10px_10px_black] -->
    <div class="absolute inset-0 blur-sm bg-black/20"></div>

    <div class="relative z-10 text-center px-4 w-[80vw] overflow-x-hidden">
      <video
        class="w-full max-w-2xl mx-auto"
        autoplay
        muted
        loop
        playsinline
        disablePictureInPicture={true}
      >
        <source src={trailer} type="video/mp4" />
        <img
          src={asset("/poster.webp")}
          title="Your browser does not support the video tag."
          alt=""
        />
      </video>
    </div>
  </section>

  <!-- Content Sections -->
  <section id="main-content-start" class="w-full h-screen">
    <About />
  </section>

  <section class="w-full h-screen">
    <CastSection />
  </section>

  <section bind:this={awardsSection} class="w-full">
    <Awards bind:this={awardsComponent} />
  </section>

  <section
    id="watch-now"
    class="w-full min-h-screen flex items-center justify-center bg-gray-900 text-white"
  >
    <WatchNow />
  </section>
</main>

<style>
  section {
    position: sticky;
    top: 0;
    width: 100%;
    min-height: 100vh;
  }
</style>
