<script lang="ts">
  import Section from "$lib/components/Section.svelte";
  import SectionTitle from "$lib/components/SectionTitle.svelte";
  import { Button } from "$lib/components/ui/button";
</script>

<Section
  class="w-full h-screen text-background! flex flex-col items-center justify-center gap-6 bg-gray-900"
>
  <SectionTitle title="watch now" color="text-background" />

  <div class="max-w-4xl text-center space-y-8">
    <!-- Main Heading -->
    <div class="space-y-4">
      <h2
        class="text-3xl md:text-4xl font-bold text-background leading-tight font-[Bebas_Neue]"
      >
        Experience the Full Documentary
      </h2>
      <p
        class="text-lg md:text-xl text-background/80 leading-relaxed font-[Poppins]"
      >
        A powerful story of courage, family, and acceptance in the South Asian
        community
      </p>
    </div>

    <!-- Watch Options -->
    <div class="grid md:grid-cols-2 gap-6 max-w-2xl mx-auto">
      <!-- Official Website -->
      <div class="bg-background/10 backdrop-blur-sm rounded-lg p-6 space-y-4">
        <h3 class="text-xl font-semibold text-background font-[Poppins]">
          Official Website
        </h3>
        <p class="text-sm text-background/70">
          Visit the official site for screenings, ordering options, and more
          information
        </p>
        <Button
          href="https://emergencefilm.net/"
          target="_blank"
          rel="noopener noreferrer"
          class="w-full bg-primary hover:bg-primary/90"
        >
          Visit emergencefilm.net
        </Button>
      </div>

      <!-- Watch & Order -->
      <div class="bg-background/10 backdrop-blur-sm rounded-lg p-6 space-y-4">
        <h3 class="text-xl font-semibold text-background font-[Poppins]">
          Order Film
        </h3>
        <p class="text-sm text-background/70">
          Stream via Vimeo VOD ($20 CAD) or order DVDs for educational use
        </p>
        <Button
          href="https://emergencefilm.net/order-film/"
          target="_blank"
          rel="noopener noreferrer"
          class="w-full bg-secondary hover:bg-secondary/90"
        >
          Order & Pricing
        </Button>
      </div>
    </div>

    <!-- Trailer & Videos -->
    <div class="bg-background/5 rounded-lg p-6 space-y-4">
      <h3 class="text-2xl font-semibold text-background font-[Poppins]">
        Trailer & Videos
      </h3>
      <p class="text-background/80">
        Watch the official trailer, behind-the-scenes content, and interviews
        with the cast and crew
      </p>
      <div class="flex flex-wrap justify-center gap-4">
        <Button
          href="https://emergencefilm.net/videos/"
          target="_blank"
          rel="noopener noreferrer"
          variant="outline"
          class="border-background/30 text-background hover:bg-background/10"
        >
          Official Trailer
        </Button>
        <Button
          href="https://emergencefilm.net/videos/"
          target="_blank"
          rel="noopener noreferrer"
          variant="outline"
          class="border-background/30 text-background hover:bg-background/10"
        >
          Behind the Scenes
        </Button>
        <Button
          href="https://emergencefilm.net/videos/"
          target="_blank"
          rel="noopener noreferrer"
          variant="outline"
          class="border-background/30 text-background hover:bg-background/10"
        >
          Interviews
        </Button>
      </div>
    </div>

    <!-- Additional Resources -->
    <div class="flex flex-wrap justify-center gap-4 text-sm">
      <a
        href="https://emergencefilm.net/download-discussion-guide/"
        target="_blank"
        rel="noopener noreferrer"
        class="text-background/60 hover:text-background underline underline-offset-2"
      >
        Discussion Guide (Free)
      </a>
      <span class="text-background/40">•</span>
      <a
        href="https://emergencefilm.net/request-a-screening/"
        target="_blank"
        rel="noopener noreferrer"
        class="text-background/60 hover:text-background underline underline-offset-2"
      >
        Request a Screening
      </a>
      <span class="text-background/40">•</span>
      <a
        href="https://emergencefilm.net/major-awards-and-official-selections/"
        target="_blank"
        rel="noopener noreferrer"
        class="text-background/60 hover:text-background underline underline-offset-2"
      >
        Awards & Festivals
      </a>
    </div>
  </div>
</Section>
