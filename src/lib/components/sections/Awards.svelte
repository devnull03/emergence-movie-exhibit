<script lang="ts">
  import { asset } from "$app/paths";
  import { onMount } from "svelte";
  import { browser } from "$app/environment";
  import Section from "$lib/components/Section.svelte";
  import SectionTitle from "$lib/components/SectionTitle.svelte";
  import emergence from "$lib/content/emergence.json";

  const stills = [
    asset("/stills/Alex Still Photo (1).jpg"),
    asset("/stills/alex-and-kayden-sitting-down-on-park-bench.webp"),
    asset("/stills/alex-in-bed.webp"),
    asset("/stills/Avtar and Rajwant Still Photo (1) (1).jpg"),
    asset("/stills/emergence-finecut-flat.00_03_59_01.still095.jpg"),
    asset("/stills/emergence-finecut-flat.00_29_59_19.still066.jpg"),
    asset("/stills/emergence-finecut-flat.00_39_23_01.still056.jpg"),
    asset("/stills/emergence-finecut-flat.00_52_15_14.still006.jpg"),
    asset("/stills/emergence-finecut-flat.01_04_44_03.still014.jpg"),
    asset("/stills/img_1888.webp"),
    asset("/stills/Jaspal Still Photo (1).jpg"),
    asset("/stills/Kayden Still Photo (1).jpg"),
    asset("/stills/Rajwant and Jag Still Photo (1).jpg"),
    asset("/stills/vinay-reading-script-notes.webp"),
  ];

  const awards = emergence.awardsHighlights;

  let currentAwardIndex = $state(0);
  let floatingImages: Array<{
    id: number;
    src: string;
    x: number;
    initialY: number;
    y: number; // dynamic y offset
    opacity: number;
    scale: number;
    isLoaded?: boolean;
  }> = $state([]);
  let imageCounter = 0;
  let imageContainer: HTMLElement;

  // Track which stills have finished loading
  const loadedSrcs = new Set<string>();
  let hasPreloaded = false;

  const preloadAllStills = () => {
    if (hasPreloaded || !browser) return;
    hasPreloaded = true;
    for (const src of stills) {
      const img = new Image();
      img.decoding = "async";
      img.src = src;
      img.onload = () => {
        loadedSrcs.add(src);
      };
      img.onerror = () => {
        // Keep going even if a particular image fails
      };
    }
  };

  // Preload on mount
  onMount(() => {
    preloadAllStills();
  });

  const getRandomStill = () => {
    const idx = Math.floor(Math.random() * stills.length);
    return stills[idx];
  };

  const addFloatingImage = (x: number, y: number) => {
    const src = getRandomStill();
    const newImage = {
      id: imageCounter++,
      src,
      x: x - 100, // Center the image on cursor
      initialY: y - 100, // Store the initial Y position
      y: 0, // Start with no scroll offset
      opacity: 0,
      scale: 0.5, // Start smaller for more dramatic effect
      isLoaded: loadedSrcs.has(src),
    };

    floatingImages = [...floatingImages, newImage];
    console.log("Created new image:", newImage, "at position:", x, y);

    // Animate in only if already loaded; otherwise wait for onload handler
    if (newImage.isLoaded) {
      requestAnimationFrame(() => {
        const index = floatingImages.findIndex((img) => img.id === newImage.id);
        if (index !== -1) {
          floatingImages[index].opacity = 1;
          floatingImages[index].scale = 1;
          floatingImages = [...floatingImages];
          console.log("Animated in image (preloaded):", floatingImages[index]);
        }
      });
    }

    // Remove after delay
    setTimeout(
      () => {
        removeImage(newImage.id);
      },
      1500 + Math.random() * 800 // Faster removal timing
    );
  };

  const removeImage = (id: number) => {
    const index = floatingImages.findIndex((img) => img.id === id);
    if (index !== -1) {
      floatingImages[index].opacity = 0;
      floatingImages[index].scale = 0.5;
      floatingImages = [...floatingImages];
      setTimeout(() => {
        floatingImages = floatingImages.filter((img) => img.id !== id);
      }, 150);
    }
  };

  const handleImageLoad = (id: number, src: string) => {
    loadedSrcs.add(src);
    const index = floatingImages.findIndex((img) => img.id === id);
    if (index !== -1) {
      floatingImages[index].isLoaded = true;
      floatingImages[index].opacity = 1;
      floatingImages[index].scale = 1;
      floatingImages = [...floatingImages];
      console.log("Animated in image (onload):", floatingImages[index]);
    }
  };

  // Handle pointer events for floating images
  let lastImageTime = 0;
  const handlePointerEvent = (e: MouseEvent | PointerEvent) => {
    if (!imageContainer) return;

    const rect = imageContainer.getBoundingClientRect();
    const clientX = e.clientX;
    const clientY = e.clientY;

    // Update cursor position for scroll-generated images
    lastCursorX = clientX - rect.left;
    lastCursorY = clientY - rect.top;

    const now = Date.now();
    if (now - lastImageTime > 150) {
      // Reduced throttle for faster response
      addFloatingImage(lastCursorX, lastCursorY);
      lastImageTime = now;
    }
  };

  // Export function to update award index from parent
  export function updateAwardIndex(index: number) {
    if (index >= 0 && index < awards.length) {
      currentAwardIndex = index;
    }
  }

  let lastScrollProgress = 0;
  let lastScrollY = 0;
  export function updateScrollProgress(progress: number) {
    // Only create an image if scroll progress has changed enough (e.g., by 0.01)
    if (Math.abs(progress - lastScrollProgress) > 0.01) {
      createScrollImages();
      lastScrollProgress = progress;
    }
    // Calculate scroll delta in px (simulate 1000px scroll range)
    const currentY = progress * 1000;
    const deltaY = lastScrollY - currentY; // invert direction
    if (deltaY !== 0) {
      floatingImages = floatingImages.map((img) => ({
        ...img,
        y: img.y + deltaY * 8,
      }));
    }
    lastScrollY = currentY;
  }

  let lastCursorX = 0;
  let lastCursorY = 0;

  let lastScrollImageTime = 0;
  const createScrollImages = () => {
    if (!imageContainer || lastCursorX === 0 || lastCursorY === 0) return;

    const now = Date.now();
    if (now - lastScrollImageTime > 200) {
      addFloatingImage(lastCursorX, lastCursorY);
      lastScrollImageTime = now;
    }
  };
</script>

<!-- Wrapper for Awards section with full-width image interaction -->
<div
  class="relative w-full h-screen bg-background text-foreground overflow-hidden"
>
  <SectionTitle title="Awards" color="text-foreground" />

  <!-- Content Section (constrained by Section wrapper) -->
  <Section class="relative w-full h-screen bg-transparent">
    <!-- Two Column Layout -->
    <div class="flex h-full flex-col md:flex-row">
      <!-- Left Column: Awards Display -->
      <div
        class="w-full md:w-1/2 flex flex-col justify-center items-start py-[6vh] z-10 min-h-full"
      >
        {#if awards[currentAwardIndex]}
          {@const award = awards[currentAwardIndex]}
          <div
            class="grid w-full"
            style="
            max-width:100%;
            grid-template-rows:
              3.2rem /* badge */
              4.5rem /* title */
              3.2rem /* festival */
              2.2rem /* date */
              3.2rem /* progress */
            ;
            row-gap: 1rem;
            min-height: 16.3rem;
          "
          >
            <!-- Award Result Badge -->
            <div class="flex items-center h-full">
              <span
                class="px-3 md:px-4 py-2 bg-primary text-primary-foreground rounded-full text-xs md:text-sm font-semibold"
                style="min-height:2.5rem;display:inline-flex;align-items:center;"
              >
                {award.result}
              </span>
            </div>

            <!-- Award Title -->
            <h3
              class="text-2xl md:text-3xl font-bold leading-tight flex items-center h-full"
              style="min-height:3.5rem;"
            >
              {award.title}
            </h3>

            <!-- Festival Name -->
            <p
              class="text-lg md:text-xl text-muted-foreground flex items-center h-full"
              style="min-height:2.5rem;"
            >
              {award.festival}
            </p>

            <!-- Date -->
            <p
              class="text-sm text-muted-foreground flex items-center h-full"
              style="min-height:1.5rem;"
            >
              {new Date(award.date).toLocaleDateString("en-US", {
                year: "numeric",
                month: "long",
                day: "numeric",
              })}
            </p>

            <!-- Progress Indicator -->
            <div
              class="flex items-center gap-2 w-full h-full"
              style="min-width:16rem;max-width:100%;min-height:2.5rem;"
            >
              <span class="text-sm text-muted-foreground whitespace-nowrap">
                {currentAwardIndex + 1} of {awards.length}
              </span>
              <div
                class="relative grow h-1 bg-muted rounded min-w-[8rem] max-w-[16rem]"
              >
                <div
                  class="h-full bg-primary rounded transition-all duration-300 absolute left-0 top-0"
                  style="width: {((currentAwardIndex + 1) / awards.length) *
                    100}%"
                ></div>
              </div>
            </div>
          </div>
        {/if}
      </div>
      <!-- Right column spacer to keep layout -->
      <div class="w-full md:w-1/2 h-1/2 md:h-full rounded-sm"></div>
    </div>
  </Section>

  <!-- Full-width interactive area for image popup (outside Section constraints) -->
  <div
    bind:this={imageContainer}
    class="absolute inset-0 w-full h-full"
    onmousemove={handlePointerEvent}
    onpointermove={handlePointerEvent}
    role="presentation"
    aria-hidden="true"
    style="cursor: none;"
  >
    <!-- Floating Images (cover entire viewport area) -->
    {#each floatingImages as image (image.id)}
      <img
        src={image.src}
        alt="Movie still"
        decoding="async"
        class="absolute aspect-video w-[50vw] md:w-[22vw] object-cover shadow-lg pointer-events-none transition-all duration-150 ease-out z-0"
        style="
            left: {image.x}px;
            top: {image.initialY + image.y}px;
            opacity: {image.opacity};
            transform: scale({image.scale});
          "
        onload={() => handleImageLoad(image.id, image.src)}
        onerror={() => removeImage(image.id)}
      />
    {/each}

    <!-- Subtle instruction text -->
    <div
      class="absolute inset-0 z-10 flex items-center justify-center pointer-events-none"
    >
      <p
        class="text-muted-foreground/30 text-base md:text-lg font-light tracking-wide text-center px-4"
      >
        <span class="hidden md:inline">Move your cursor to reveal stills</span>
        <span class="md:hidden">Tap to reveal stills</span>
      </p>
    </div>
  </div>
</div>
