<script lang="ts">
  import Section from "$lib/components/Section.svelte";
  import SectionTitle from "$lib/components/SectionTitle.svelte";
  import { Button } from "$lib/components/ui/button";
</script>

<Section
  class="w-full h-screen text-background! bg-gray-900 *:h-full"
>
  <SectionTitle title="watch now" color="text-background" />

  <div class="max-w-6xl mx-auto px-4 h-full flex flex-col justify-center items-center gap-6">
    <!-- Main Heading -->
    <div class="text-center">
      <h2
        class="text-2xl md:text-3xl font-bold text-background leading-tight font-[Bebas_Neue]"
      >
        Experience the Full Documentary
      </h2>
      <p
        class="text-base md:text-lg text-background/80 leading-relaxed font-[Poppins]"
      >
        A powerful story of courage, family, and acceptance in the South Asian
        community
      </p>
    </div>

    <!-- Bento Grid Layout -->
    <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4">
      <!-- Watch Full Movie - Large Card -->
      <div
        class="md:col-span-2 lg:col-span-2 bg-background/10 rounded-xl p-6 flex flex-col justify-between hover:bg-background/15 transition-colors"
      >
        <div>
          <h3 class="text-2xl font-bold text-background mb-2 font-[Bebas_Neue]">
            Watch Full Movie
          </h3>
          <p class="text-background/70 mb-4">
            Stream the complete documentary on the official website
          </p>
          <div class="space-y-2 text-sm text-background/60">
            <p>• Available via Vimeo VOD</p>
            <p>• $20 CAD streaming price</p>
            <p>• Instant access after purchase</p>
          </div>
        </div>
        <Button
          href="https://emergencefilm.net/"
          target="_blank"
          rel="noopener noreferrer"
        >
          Watch Now
        </Button>
      </div>

      <!-- Order Film - Medium Card -->
      <div
        class="bg-background/8 rounded-xl p-6 flex flex-col justify-between hover:bg-background/12 transition-colors"
      >
        <div>
          <h3 class="text-xl font-bold text-background mb-2 font-[Bebas_Neue]">
            Order Film
          </h3>
          <p class="text-background/70 text-sm mb-3">
            Physical DVDs for educational institutions
          </p>
          <div class="text-xs text-background/60 space-y-1">
            <p>• Educational licensing</p>
            <p>• Bulk orders available</p>
          </div>
        </div>
        <Button
          href="https://emergencefilm.net/order-film/"
          target="_blank"
          rel="noopener noreferrer"
        >
          Order
        </Button>
      </div>

      <!-- Trailer & Videos - Tall Card -->
      <div
        class="lg:row-span-2 bg-background/6 rounded-xl p-6 flex flex-col justify-between hover:bg-background/10 transition-colors"
      >
        <div>
          <h3 class="text-xl font-bold text-background mb-2 font-[Bebas_Neue]">
            Trailer & Videos
          </h3>
          <p class="text-background/70 text-sm mb-4">
            Watch preview content and behind-the-scenes
          </p>
          <div class="space-y-2 text-xs text-background/60">
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
        >
          Watch Videos
        </Button>
      </div>

      <!-- Request Screening - Medium Card -->
      <div
        class="md:col-span-2 lg:col-span-1 bg-background/8 rounded-xl p-6 flex flex-col justify-between hover:bg-background/12 transition-colors"
      >
        <div>
          <h3 class="text-xl font-bold text-background mb-2 font-[Bebas_Neue]">
            Request Screening
          </h3>
          <p class="text-background/70 text-sm mb-3">
            Host a community screening event
          </p>
          <div class="text-xs text-background/60 space-y-1">
            <p>• Educational institutions</p>
            <p>• Community centers</p>
            <p>• Cultural organizations</p>
          </div>
        </div>
        <Button
          href="https://emergencefilm.net/request-a-screening/"
          target="_blank"
          rel="noopener noreferrer"
        >
          Request
        </Button>
      </div>

      <!-- Additional Resources - Wide Card -->
      <div
        class="md:col-span-2 lg:col-span-2 bg-background/5 rounded-xl p-6 flex flex-col justify-between hover:bg-background/8 transition-colors"
      >
        <div>
          <h3 class="text-lg font-bold text-background mb-2 font-[Bebas_Neue]">
            Additional Resources
          </h3>
          <div
            class="grid grid-cols-1 md:grid-cols-3 gap-3 text-xs text-background/70"
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
        <div class="flex flex-wrap gap-2">
          <Button
            href="https://emergencefilm.net/download-discussion-guide/"
            target="_blank"
            rel="noopener noreferrer"
          >
            Download Guide
          </Button>
          <Button
            href="https://emergencefilm.net/major-awards-and-official-selections/"
            target="_blank"
            rel="noopener noreferrer"
          >
            View Awards
          </Button>
        </div>
      </div>
    </div>
  </div>
</Section>
