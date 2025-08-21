<script lang="ts">
  import { onMount } from "svelte";
  import emergenceData from "$lib/content/films/emergence.json";

  let innerHeight: number;
  let innerWidth: number;
  let background_container: HTMLDivElement;
  let scrolling_container: HTMLDivElement;

  // Section background mapping - using poster colors
  const section_backgrounds = {
    hero: "linear-gradient(135deg, #0ea568 0%, #5b2d83 50%, #225c9e 100%)",
    synopsis: "#f8fafc",
    trailer: "#0b0b0c",
    watch: "#f8fafc", 
    spotlights: "#0b0b0c",
    awards: "#f8fafc",
    guide: "#0b0b0c",
    sources: "#f8fafc"
  };

  let current_section = "hero";

  const scroll_handler = (e: UIEvent) => {
    let current_section_id = find_inview_section();
    if (Object.keys(section_backgrounds).includes(current_section_id)) {
      if (current_section_id !== current_section) {
        current_section = current_section_id;
      }
    }
  };

  const find_inview_section = () => {
    if (!innerWidth || !innerHeight) return "hero";
    let elements = document.elementsFromPoint(innerWidth / 2, innerHeight / 2);
    let section = elements.find((el) => el.id && Object.keys(section_backgrounds).includes(el.id));
    return section?.id || "hero";
  };

  onMount(() => {
    // Smooth scroll to sections
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function (e) {
        e.preventDefault();
        const href = this.getAttribute('href');
        if (href && href !== '#') {
          const target = document.querySelector(href);
          if (target) {
            target.scrollIntoView({
              behavior: 'smooth',
              block: 'start'
            });
          }
        }
      });
    });
  });
</script>

<svelte:window bind:innerHeight bind:innerWidth on:scroll={scroll_handler} />

<svelte:head>
  <title>Emergence: Out of the Shadows - SACDA Digital Exhibit</title>
  <meta name="description" content="An intimate documentary following three South Asian LGBTQ+ individuals as they navigate identity, family, and belonging. Winner of 7 awards across 51 international film festivals." />
  <meta property="og:title" content="Emergence: Out of the Shadows - Digital Exhibit" />
  <meta property="og:description" content="Discover the powerful stories of Kayden, Jag, and Amar in this acclaimed documentary." />
</svelte:head>

<main class="relative bg-gray-100">
  <!-- Sticky Background -->
  <div class="fixed top-0 left-0 w-full h-full -z-10">
    <div class="w-full h-full transition-all duration-700 ease-out" 
         style="background: {section_backgrounds[current_section]}"
         bind:this={background_container}>
    </div>
  </div>

  <!-- Scrolling Content -->
  <div class="relative z-10" bind:this={scrolling_container}>

    <!-- Hero Section -->
    <section id="hero" class="min-h-screen flex items-center justify-center text-white">
      <div class="text-center max-w-4xl mx-auto px-8">
        <div class="bg-black bg-opacity-50 p-12 backdrop-blur-sm">
          <h1 class="text-6xl md:text-8xl font-bold mb-4 leading-tight font-mono">
            EMERGENCE
          </h1>
          <p class="text-2xl md:text-3xl mb-8 font-light">
            Out of the Shadows
          </p>
          <p class="text-lg mb-12 max-w-2xl mx-auto leading-relaxed">
            An intimate documentary following three South Asian LGBTQ+ individuals as they navigate identity, family, and belonging
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <a href="#trailer" 
               class="bg-emerald-500 hover:bg-emerald-600 text-white px-8 py-4 font-bold transition-all duration-300 transform hover:scale-105">
              Watch Trailer
            </a>
            <a href="#synopsis"
               class="border-2 border-white text-white hover:bg-white hover:text-black px-8 py-4 font-bold transition-all duration-300">
              Explore Story
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Synopsis Section -->
    <section id="synopsis" class="section-content">
      <div class="content-box">
        <h2 class="section-title">The Story</h2>
        <p class="text-lg leading-relaxed mb-8">
          {emergenceData.synopsis}
        </p>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mt-12">
          <div class="stat-box">
            <div class="stat-number">51</div>
            <div class="stat-label">Festival Selections</div>
          </div>
          <div class="stat-box">
            <div class="stat-number">7</div>
            <div class="stat-label">Award Wins</div>
          </div>
          <div class="stat-box">
            <div class="stat-number">4</div>
            <div class="stat-label">Languages</div>
          </div>
          <div class="stat-box">
            <div class="stat-number">81</div>
            <div class="stat-label">Minutes (Full)</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Trailer Section -->
    <section id="trailer" class="section-content bg-black text-white">
      <div class="content-box">
        <h2 class="section-title text-white">Watch Trailer</h2>
        <div class="aspect-video bg-gray-800 flex items-center justify-center">
          <iframe 
            class="w-full h-full" 
            src="https://www.youtube.com/embed/{emergenceData.trailer.youtubeId}" 
            title="Emergence: Out of the Shadows Trailer"
            frameborder="0" 
            allowfullscreen
            loading="lazy">
          </iframe>
        </div>
      </div>
    </section>

    <!-- Watch the Film Section -->
    <section id="watch" class="section-content">
      <div class="content-box">
        <h2 class="section-title">Watch the Film</h2>
        <p class="text-lg mb-12">Available in multiple versions and languages</p>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          {#each emergenceData.versions as version}
            <div class="film-card">
              <h3 class="text-xl font-bold mb-4">{version.title}</h3>
              <div class="mb-4">
                <span class="badge">Runtime: {version.runtime}</span>
                <span class="badge ml-2">Language: {version.lang}</span>
              </div>
              <a href="https://youtube.com/watch?v={version.id}" 
                 target="_blank" 
                 rel="noopener noreferrer"
                 class="cta-button">
                Watch on YouTube →
              </a>
            </div>
          {/each}
        </div>
      </div>
    </section>

    <!-- Cast Spotlights Section -->
    <section id="spotlights" class="section-content bg-black text-white">
      <div class="content-box">
        <h2 class="section-title text-white">Cast Spotlights</h2>
        <p class="text-lg mb-12 text-gray-300">Personal stories from our three protagonists</p>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          {#each emergenceData.castSpotlights as cast}
            <div class="cast-card">
              <h3 class="text-2xl font-bold mb-4">{cast.name}</h3>
              <p class="text-gray-300 mb-6 leading-relaxed">{cast.bio}</p>
              <div class="mb-4">
                <span class="badge">Runtime: {cast.runtime}</span>
              </div>
              <a href="https://youtube.com/watch?v={cast.youtubeId}" 
                 target="_blank" 
                 rel="noopener noreferrer"
                 class="cta-button-white">
                Watch Story →
              </a>
            </div>
          {/each}
        </div>
      </div>
    </section>

    <!-- Awards Section -->
    <section id="awards" class="section-content">
      <div class="content-box">
        <h2 class="section-title">Recognition & Awards</h2>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mb-12">
          <div class="award-stat">
            <div class="award-number">{emergenceData.awardsSummary.countsByResult.totalOfficialSelections}</div>
            <div class="award-label">Festival Selections</div>
          </div>
          <div class="award-stat">
            <div class="award-number">{emergenceData.awardsSummary.countsByResult.awardWinner}</div>
            <div class="award-label">Award Wins</div>
          </div>
          <div class="award-stat">
            <div class="award-number">{emergenceData.awardsSummary.countsByResult.finalist}</div>
            <div class="award-label">Finalists</div>
          </div>
          <div class="award-stat">
            <div class="award-number">{emergenceData.awardsSummary.countsByFestivalType.lgbtq}</div>
            <div class="award-label">LGBTQ+ Festivals</div>
          </div>
        </div>

        <div class="mb-12">
          <h3 class="text-2xl font-bold mb-8">Award Highlights</h3>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            {#each emergenceData.awardsHighlights.slice(0, 6) as award}
              <div class="award-card">
                <div class="award-result">{award.result}</div>
                <div class="award-title">{award.title}</div>
                <div class="award-festival">{award.festival}</div>
              </div>
            {/each}
          </div>
        </div>

        <div class="text-center">
          <h3 class="text-xl font-bold mb-4">Major Qualifying Festivals</h3>
          <div class="flex flex-wrap justify-center gap-4">
            <span class="qualifier-badge">Academy Award Qualifying</span>
            <span class="qualifier-badge">BAFTA Qualifying</span>
            <span class="qualifier-badge">Canadian Screen Award Qualifying</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Teacher's Guide Section -->
    <section id="guide" class="section-content bg-black text-white">
      <div class="content-box">
        <h2 class="section-title text-white">Educational Resources</h2>
        <div class="text-center max-w-md mx-auto">
          <h3 class="text-2xl font-bold mb-4">Teacher's Discussion Guide</h3>
          <p class="text-gray-300 mb-6">Comprehensive educational materials for classroom discussion</p>
          <a href="{emergenceData.teacherGuide.href}" 
             target="_blank" 
             rel="noopener noreferrer"
             class="cta-button-white">
            Download Guide →
          </a>
        </div>
      </div>
    </section>

    <!-- Sources and Rights Section -->
    <section id="sources" class="section-content">
      <div class="content-box">
        <h2 class="section-title">Sources & Rights</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
          <div>
            <h3 class="text-xl font-bold mb-4">Official Links</h3>
            <ul class="space-y-3">
              <li><a href="https://emergencefilm.net/" target="_blank" class="text-emerald-600 hover:text-emerald-700">Official Film Website →</a></li>
              <li><a href="https://sacda.ca" target="_blank" class="text-emerald-600 hover:text-emerald-700">SACDA Archive →</a></li>
            </ul>
          </div>
          <div>
            <h3 class="text-xl font-bold mb-4">Usage Rights</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              For screening, distribution, or related inquiries, contact info@shervancouver.com. 
              Third parties must obtain prior written permission to use documentary materials. 
              Unauthorized use is strictly prohibited.
            </p>
            <a href="mailto:info@shervancouver.com" class="text-emerald-600 hover:text-emerald-700">
              Contact for Rights →
            </a>
          </div>
        </div>
      </div>
    </section>

  </div>
</main>

<style>
  .section-content {
    min-height: 100vh;
    padding: 5rem 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .content-box {
    max-width: 72rem;
    margin: 0 auto;
    /* Flat design - no rounded corners, minimal shadows */
    clip-path: polygon(
      0% 0%, 
      98% 0%, 
      100% 2%, 
      100% 98%, 
      98% 100%, 
      2% 100%, 
      0% 98%, 
      0% 2%
    );
    background: rgba(255, 255, 255, 0.95);
    padding: 3rem;
  }

  .section-content.bg-black .content-box {
    background: rgba(0, 0, 0, 0.95);
  }

  .section-title {
    font-size: 2.5rem;
    font-weight: bold;
    text-align: center;
    margin-bottom: 3rem;
    color: #374151;
    font-family: monospace;
  }

  .stat-box {
    text-align: center;
    padding: 1.5rem;
    border: 1px solid #10b981;
    background-color: #ecfdf5;
  }

  .stat-number {
    font-size: 1.875rem;
    font-weight: bold;
    color: #10b981;
  }

  .stat-label {
    font-size: 0.875rem;
    color: #6b7280;
    margin-top: 0.5rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .film-card, .cast-card {
    padding: 1.5rem;
    border: 1px solid #d1d5db;
    background: white;
  }

  .cast-card {
    background: #1f2937;
    border-color: #4b5563;
    color: white;
  }

  .badge {
    display: inline-block;
    background: #e5e7eb;
    color: #1f2937;
    padding: 0.25rem 0.75rem;
    font-size: 0.875rem;
  }

  .cast-card .badge {
    background: #4b5563;
    color: #e5e7eb;
  }

  .cta-button {
    display: inline-block;
    background: #10b981;
    color: white;
    padding: 0.75rem 1.5rem;
    font-weight: bold;
    transition: background-color 0.3s;
  }

  .cta-button:hover {
    background: #059669;
  }

  .cta-button-white {
    display: inline-block;
    background: white;
    color: black;
    padding: 0.75rem 1.5rem;
    font-weight: bold;
    transition: background-color 0.3s;
  }

  .cta-button-white:hover {
    background: #f3f4f6;
  }

  .award-stat {
    text-align: center;
  }

  .award-number {
    font-size: 1.875rem;
    font-weight: bold;
    color: #10b981;
  }

  .award-label {
    font-size: 0.875rem;
    color: #6b7280;
    margin-top: 0.5rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .award-card {
    padding: 1rem;
    border: 1px solid #a7f3d0;
    background: #ecfdf5;
  }

  .award-result {
    color: #10b981;
    font-weight: bold;
    font-size: 0.875rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .award-title {
    font-weight: bold;
    color: #1f2937;
    margin-top: 0.25rem;
  }

  .award-festival {
    color: #6b7280;
    font-size: 0.875rem;
    margin-top: 0.25rem;
  }

  .qualifier-badge {
    background: #10b981;
    color: white;
    padding: 0.5rem 1rem;
    font-size: 0.875rem;
    font-weight: bold;
  }
</style>
