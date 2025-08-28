<script lang="ts">
  import { onMount, onDestroy } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger, ScrollSmoother } from "gsap/all";
  import emergenceData from "$lib/content/films/emergence.json";

  let smoother: globalThis.ScrollSmoother | undefined = $state();

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

    smoother = ScrollSmoother.create({
      smooth: 2,
      effects: true,
      smoothTouch: true,
      normalizeScroll: true,
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

<!-- <div class="smooth-wrapper"> -->
  <main class="bg-blue-200 h-screen">
    ajldf
  </main>
<!-- </div> -->
