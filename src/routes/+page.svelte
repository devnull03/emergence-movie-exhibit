<script lang="ts">
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger, ScrollToPlugin } from "gsap/all";
  import CastSection from "$lib/components/sections/CastSection.svelte";
  import About from "$lib/components/sections/About.svelte";
  import trailer from "$lib/assets/trailer.mp4";
  import { asset } from "$app/paths";

  // Parallax scroll state
  let y = $state(0);

  const stills = [
    { src: asset("/stills/Alex Still Photo (1).jpg"), speed: 1.01 },
    {
      src: asset("/stills/Avtar and Rajwant Still Photo (1) (1).jpg"),
      speed: 1.2,
    },
    { src: asset("/poster.webp"), speed: 1.25 },
    { src: asset("/stills/Jaspal Still Photo (1).jpg"), speed: 1 },
    { src: asset("/stills/Kayden Still Photo (1).jpg"), speed: 1.2 },
    { src: asset("/stills/Rajwant and Jag Still Photo (1).jpg"), speed: 1.2 },
  ];

  // let smoother: globalThis.ScrollSmoother | undefined = $state();

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

<svelte:window bind:scrollY={y} />

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

    <section class="w-full grid grid-cols-3 relative! bg-transparent! -mb-54">
      {#each stills as still, i}
        <img
          src={still.src}
          alt="Film Still"
          class="object-cover z-50 h-full"
          class:row-span-2={i === 2}
          class:col-start-3={i === 5}
          data-speed={still.speed}
        />
      {/each}
    </section>

  <section class="w-full h-screen">
    <CastSection />
  </section>

  <section
    class="w-full min-h-screen flex items-center justify-center bg-gray-100"
  >
    <div class="text-gray-900 text-3xl font-bold">
      [Placeholder: Awards & Recognition]
    </div>
  </section>

  <section
    id="watch-now"
    class="w-full min-h-screen flex items-center justify-center bg-gray-900 text-white"
  >
    <div class="text-white text-3xl font-bold">[Placeholder: Watch Now]</div>
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
