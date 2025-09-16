<script lang="ts">
  import { asset } from "$app/paths";
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
    opacity: number;
    scale: number;
  }> = $state([]);
  let imageCounter = 0;
  let imageContainer: HTMLElement;

  const getRandomStill = () => {
    const idx = Math.floor(Math.random() * stills.length);
    return stills[idx];
  };

  const addFloatingImage = (x: number, y: number) => {
    const newImage = {
      id: imageCounter++,
      src: getRandomStill(),
      x: x - 100, // Center the image on cursor
      initialY: y - 100, // Store the initial Y position
      opacity: 0,
      scale: 0.5, // Start smaller for more dramatic effect
    };

    floatingImages = [...floatingImages, newImage];
    console.log("Created new image:", newImage, "at position:", x, y);

    // Animate in immediately with faster timing
    requestAnimationFrame(() => {
      const index = floatingImages.findIndex((img) => img.id === newImage.id);
      if (index !== -1) {
        floatingImages[index].opacity = 1;
        floatingImages[index].scale = 1;
        floatingImages = [...floatingImages];
        console.log("Animated in image:", floatingImages[index]);
      }
    });

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

  // Update scroll position for scroll-based image creation
  export function updateScrollProgress(progress: number) {
    createScrollImages();
  }

  // Track cursor position
  let lastCursorX = 0;
  let lastCursorY = 0;

  // Create images automatically on scroll at cursor position
  let lastScrollImageTime = 0;
  const createScrollImages = () => {
    if (!imageContainer || lastCursorX === 0 || lastCursorY === 0) return;

    const now = Date.now();
    if (now - lastScrollImageTime > 200) {
      // Throttle image creation on scroll
      // Use last known cursor position
      addFloatingImage(lastCursorX, lastCursorY);
      lastScrollImageTime = now;
    }
  };
</script>

<SectionTitle title="Awards" color="text-foreground" />
<Section
  class="relative w-full h-screen bg-background text-foreground overflow-hidden"
>
  <!-- Two Column Layout -->
  <div class="flex h-full flex-col md:flex-row max-w-5xl mx-auto">
    <!-- Left Column: Awards Display -->
    <div
      class="w-full md:w-1/2 flex flex-col justify-center items-start px-8 md:px-16 py-8 z-10"
    >
      {#if awards[currentAwardIndex]}
        {@const award = awards[currentAwardIndex]}
        <div class="space-y-4 md:space-y-6 max-w-lg">
          <!-- Award Result Badge -->
          <div class="inline-block">
            <span
              class="px-3 md:px-4 py-2 bg-primary text-primary-foreground rounded-full text-xs md:text-sm font-semibold"
            >
              {award.result}
            </span>
          </div>

          <!-- Award Title -->
          <h3 class="text-2xl md:text-3xl font-bold leading-tight">
            {award.title}
          </h3>

          <!-- Festival Name -->
          <p class="text-lg md:text-xl text-muted-foreground">
            {award.festival}
          </p>

          <!-- Date -->
          <p class="text-sm text-muted-foreground">
            {new Date(award.date).toLocaleDateString("en-US", {
              year: "numeric",
              month: "long",
              day: "numeric",
            })}
          </p>

          <!-- Progress Indicator -->
          <div class="flex items-center space-x-2 mt-6 md:mt-8">
            <span class="text-sm text-muted-foreground">
              {currentAwardIndex + 1} of {awards.length}
            </span>
            <div class="flex-1 h-1 bg-muted rounded">
              <div
                class="h-full bg-primary rounded transition-all duration-300"
                style="width: {((currentAwardIndex + 1) / awards.length) *
                  100}%"
              ></div>
            </div>
          </div>
        </div>
      {/if}
    </div>

    <!-- Right Column: Interactive Image Area -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div
      bind:this={imageContainer}
      class="relative w-full md:w-1/2 h-1/2 md:h-full rounded-sm"
      onmousemove={handlePointerEvent}
      onpointermove={handlePointerEvent}
      style="cursor: none;"
    >
      <!-- Floating Images -->
      {#each floatingImages as image (image.id)}
        <img
          src={image.src}
          alt="Movie still"
          class="absolute w-32 h-20 md:w-48 md:h-32 object-cover shadow-lg pointer-events-none transition-all duration-150 ease-out"
          style="
              left: {image.x}px; 
              top: {image.initialY}px; 
              opacity: {image.opacity}; 
              transform: scale({image.scale});
              z-index: 1000;
            "
        />
      {/each}

      <!-- Subtle instruction text -->
      <div
        class="absolute inset-0 flex items-center justify-center pointer-events-none"
      >
        <p
          class="text-muted-foreground/30 text-base md:text-lg font-light tracking-wide text-center px-4"
        >
          <span class="hidden md:inline">Move your cursor to reveal stills</span
          >
          <span class="md:hidden">Tap to reveal stills</span>
        </p>
      </div>
    </div>
  </div>
</Section>
