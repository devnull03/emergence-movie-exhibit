<script lang="ts">
  import Section from "$lib/components/Section.svelte";
  import SectionTitle from "$lib/components/SectionTitle.svelte";
  import { Button } from "$lib/components/ui/button";
  import { IsMobile } from "$lib/hooks/is-mobile.svelte.ts";

  const isMobile = new IsMobile();
</script>

<Section
  class="w-full {isMobile.current
    ? 'min-h-screen py-8'
    : 'h-screen'} text-background! bg-gray-900 *:h-full overflow-y-auto"
>
  <SectionTitle title="watch now" color="text-background" />

  <div
    class="max-w-6xl mx-auto px-4 h-full flex flex-col justify-center items-center gap-6"
  >
    <!-- Main Heading -->
    <div class="text-center">
      <h2
        class="{isMobile.current
          ? 'text-xl'
          : 'text-2xl md:text-3xl'} font-bold text-background leading-tight font-[Bebas_Neue]"
      >
        Experience the Full Documentary
      </h2>
      <p
        class="{isMobile.current
          ? 'text-sm'
          : 'text-base md:text-lg'} text-background/80 leading-relaxed font-[Poppins]"
      >
        A powerful story of courage, family, and acceptance in the South Asian
        community
      </p>
    </div>

    <!-- Bento Grid Layout -->
    <div
      class="grid {isMobile.current
        ? 'grid-cols-1 gap-4'
        : 'grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4'}"
    >
      <!-- Watch Full Movie - Large Card -->
      <div
        class="{isMobile.current
          ? ''
          : 'md:col-span-2 lg:col-span-2'} bg-background/10 rounded-xl p-6 flex flex-col justify-between hover:bg-background/15 transition-colors"
      >
        <div>
          <h3
            class="{isMobile.current
              ? 'text-xl'
              : 'text-2xl'} font-bold text-background mb-2 font-[Bebas_Neue]"
          >
            Watch Full Movie
          </h3>
          <p
            class="text-background/70 mb-4 {isMobile.current ? 'text-sm' : ''}"
          >
            Stream the complete documentary on the official website
          </p>
          <div
            class="space-y-2 {isMobile.current
              ? 'text-xs'
              : 'text-sm'} text-background/60"
          >
            <p>• Available via Vimeo VOD</p>
            <p>• $20 CAD streaming price</p>
            <p>• Instant access after purchase</p>
          </div>
        </div>
        <Button
          href="https://emergencefilm.net/"
          target="_blank"
          rel="noopener noreferrer"
          class="mt-4"
        >
          Watch Now
        </Button>
      </div>

      <!-- Order Film - Medium Card -->
      <div
        class="bg-background/8 rounded-xl p-6 flex flex-col justify-between hover:bg-background/12 transition-colors"
      >
        <div>
          <h3
            class="{isMobile.current
              ? 'text-lg'
              : 'text-xl'} font-bold text-background mb-2 font-[Bebas_Neue]"
          >
            Order Film
          </h3>
          <p
            class="text-background/70 {isMobile.current
              ? 'text-xs'
              : 'text-sm'} mb-3"
          >
            Physical DVDs for educational institutions
          </p>
          <div
            class="{isMobile.current
              ? 'text-2xs'
              : 'text-xs'} text-background/60 space-y-1"
          >
            <p>• Educational licensing</p>
            <p>• Bulk orders available</p>
          </div>
        </div>
        <Button
          href="https://emergencefilm.net/order-film/"
          target="_blank"
          rel="noopener noreferrer"
          class="mt-4"
        >
          Order
        </Button>
      </div>

      <!-- Trailer & Videos - Tall Card -->
      <div
        class="{isMobile.current
          ? ''
          : 'lg:row-span-2'} bg-background/6 rounded-xl p-6 flex flex-col justify-between hover:bg-background/10 transition-colors"
      >
        <div>
          <h3
            class="{isMobile.current
              ? 'text-lg'
              : 'text-xl'} font-bold text-background mb-2 font-[Bebas_Neue]"
          >
            Trailer & Videos
          </h3>
          <p
            class="text-background/70 {isMobile.current
              ? 'text-xs'
              : 'text-sm'} mb-4"
          >
            Watch preview content and behind-the-scenes
          </p>
          <div
            class="space-y-2 {isMobile.current
              ? 'text-2xs'
              : 'text-xs'} text-background/60"
          >
            <p>• Official trailer</p>
            <p>• Behind-the-scenes footage</p>
            <p>• Cast & crew interviews</p>
            <p>• Director's commentary</p>
            <p>• Festival highlights</p>
          </div>
        </div>
        <Button
          href="https://emergencefilm.net/videos/"
          target="_blank"
          rel="noopener noreferrer"
          class="mt-4"
        >
          Watch Videos
        </Button>
      </div>

      <!-- Request Screening - Medium Card -->
      <div
        class="{isMobile.current
          ? ''
          : 'md:col-span-2 lg:col-span-1'} bg-background/8 rounded-xl p-6 flex flex-col justify-between hover:bg-background/12 transition-colors"
      >
        <div>
          <h3
            class="{isMobile.current
              ? 'text-lg'
              : 'text-xl'} font-bold text-background mb-2 font-[Bebas_Neue]"
          >
            Request Screening
          </h3>
          <p
            class="text-background/70 {isMobile.current
              ? 'text-xs'
              : 'text-sm'} mb-3"
          >
            Host a community screening event
          </p>
          <div
            class="{isMobile.current
              ? 'text-2xs'
              : 'text-xs'} text-background/60 space-y-1"
          >
            <p>• Educational institutions</p>
            <p>• Community centers</p>
            <p>• Cultural organizations</p>
          </div>
        </div>
        <Button
          href="https://emergencefilm.net/request-a-screening/"
          target="_blank"
          rel="noopener noreferrer"
          class="mt-4"
        >
          Request
        </Button>
      </div>

      <!-- Additional Resources - Wide Card -->
      <div
        class="{isMobile.current
          ? ''
          : 'md:col-span-2 lg:col-span-2'} bg-background/5 rounded-xl p-6 flex flex-col justify-between hover:bg-background/8 transition-colors"
      >
        <div>
          <h3
            class="{isMobile.current
              ? 'text-base'
              : 'text-lg'} font-bold text-background mb-2 font-[Bebas_Neue]"
          >
            Additional Resources
          </h3>
          <div
            class="grid grid-cols-1 {isMobile.current
              ? 'gap-2'
              : 'md:grid-cols-3 gap-3'} {isMobile.current
              ? 'text-2xs'
              : 'text-xs'} text-background/70"
          >
            <div>
              <p class="font-medium text-background/80">Discussion Guide</p>
              <p>Free educational resource</p>
            </div>
            <div>
              <p class="font-medium text-background/80">Awards & Recognition</p>
              <p>Film festival selections</p>
            </div>
            <div>
              <p class="font-medium text-background/80">Press Kit</p>
              <p>Media resources available</p>
            </div>
          </div>
        </div>
        <div
          class="flex {isMobile.current
            ? 'flex-col gap-2'
            : 'flex-wrap gap-2'} mt-4"
        >
          <Button
            href="https://emergencefilm.net/download-discussion-guide/"
            target="_blank"
            rel="noopener noreferrer"
            class={isMobile.current ? "text-xs" : ""}
          >
            Download Guide
          </Button>
          <Button
            href="https://emergencefilm.net/major-awards-and-official-selections/"
            target="_blank"
            rel="noopener noreferrer"
            class={isMobile.current ? "text-xs" : ""}
          >
            View Awards
          </Button>
        </div>
      </div>
    </div>
  </div>
</Section>
