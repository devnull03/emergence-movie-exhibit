<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
</script>

<svelte:head>
  <title>Cast Spotlights - Emergence: Out of the Shadows</title>
  <meta name="description" content="Personal stories from Amar, Jag, and Kayden - the cast of Emergence: Out of the Shadows documentary" />
</svelte:head>

<main class="bg-gray-100">
  <!-- Hero Section -->
  <section class="bg-black text-white relative overflow-hidden">
    <div class="absolute inset-0" style="background: linear-gradient(135deg, #5b2d83 0%, #225c9e 50%, #0ea568 100%);"></div>
    <div class="absolute inset-0 bg-black opacity-50"></div>
    
    <div class="relative z-10 max-w-6xl mx-auto px-8 py-24 text-center">
      <h1 class="text-5xl md:text-7xl font-mono font-bold mb-8 leading-tight">
        CAST<br>SPOTLIGHTS
      </h1>
      <p class="text-xl md:text-2xl mb-12 max-w-3xl mx-auto leading-relaxed">
        Personal stories from Amar, Jag, and Kayden - courageous individuals who shared their journeys of identity, acceptance, and love
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-2xl mx-auto">
        {#each emergenceData.castSpotlights as cast}
          <div class="cast-hero-stat">
            <div class="cast-name">{cast.name}</div>
            <div class="cast-runtime">{cast.runtime}</div>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- Cast Stories Grid -->
  <section class="py-20">
    <div class="max-w-7xl mx-auto px-8">
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-12">
        {#each emergenceData.castSpotlights as cast, index}
          <div class="cast-story-card">
            <!-- Story Header -->
            <div class="story-header">
              <div class="story-number">{String(index + 1).padStart(2, '0')}</div>
              <div class="story-meta">
                <h2 class="story-name">{cast.name}</h2>
                <div class="story-duration">{cast.runtime}</div>
              </div>
            </div>
            
            <!-- Story Content -->
            <div class="story-content">
              <p class="story-bio">{cast.bio}</p>
              
              <!-- Watch Link -->
              <div class="story-actions">
                <a href="https://youtube.com/watch?v={cast.youtubeId}" 
                   target="_blank" 
                   rel="noopener noreferrer"
                   class="story-watch-btn">
                  Watch {cast.name}'s Story →
                </a>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- About Section -->
  <section class="bg-black text-white py-20">
    <div class="max-w-6xl mx-auto px-8">
      <h2 class="section-heading text-white">About the Stories</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
        <div class="about-panel">
          <h3 class="panel-title">Individual Journeys</h3>
          <p class="panel-text">
            Each cast member brings their unique perspective to the documentary, sharing intimate details 
            about their experiences with family, community, and self-acceptance. These personal narratives 
            form the heart of the documentary's emotional impact.
          </p>
        </div>
        
        <div class="about-panel">
          <h3 class="panel-title">Shared Experiences</h3>
          <p class="panel-text">
            While each story is unique, the cast members share common themes of courage, resilience, 
            and the complex navigation of identity within conservative cultural contexts. Their stories 
            provide hope and representation for others facing similar challenges.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Privacy Notice -->
  <section class="bg-amber-100 border-t-4 border-amber-500">
    <div class="max-w-4xl mx-auto px-8 py-12">
      <div class="flex items-start">
        <div class="privacy-icon">⚠</div>
        <div>
          <h3 class="privacy-title">Privacy Notice</h3>
          <p class="privacy-text">
            As per director requirements, Christine Michelle Lord's photo and biographical information 
            are excluded from this cast page in accordance with the official website guidelines.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Call to Action -->
  <section class="bg-emerald-600 text-white py-20">
    <div class="max-w-4xl mx-auto text-center px-8">
      <h2 class="text-4xl font-bold mb-8">Experience Their Full Stories</h2>
      <p class="text-xl mb-12">
        Watch the complete documentary to see how these individual journeys weave together.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <a href="/" class="bg-white text-emerald-600 px-8 py-4 font-bold hover:bg-gray-100 transition-colors">
          Watch Full Documentary
        </a>
        <a href="https://emergencefilm.net/" 
           target="_blank" 
           rel="noopener noreferrer"
           class="border-2 border-white text-white hover:bg-white hover:text-emerald-600 px-8 py-4 font-bold transition-colors">
          Official Website →
        </a>
      </div>
    </div>
  </section>
</main>

<style>
  .cast-hero-stat {
    text-align: center;
  }

  .cast-name {
    font-size: 1.5rem;
    font-weight: bold;
    color: #10b981;
    font-family: monospace;
  }

  .cast-runtime {
    font-size: 0.875rem;
    color: #d1d5db;
    margin-top: 0.5rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .cast-story-card {
    background: white;
    overflow: hidden;
    transition: transform 0.3s ease;
  }

  .cast-story-card:hover {
    transform: translateY(-8px);
  }

  .story-header {
    padding: 2rem;
    background: #f8fafc;
    border-bottom: 2px solid #10b981;
    display: flex;
    align-items: center;
    gap: 1.5rem;
  }

  .story-number {
    font-size: 3rem;
    font-weight: bold;
    color: #10b981;
    font-family: monospace;
    line-height: 1;
  }

  .story-name {
    font-size: 2rem;
    font-weight: bold;
    color: #1f2937;
    margin-bottom: 0.5rem;
  }

  .story-duration {
    font-size: 0.875rem;
    color: #6b7280;
    font-family: monospace;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .story-content {
    padding: 2rem;
  }

  .story-bio {
    font-size: 1.125rem;
    color: #374151;
    line-height: 1.7;
    margin-bottom: 2rem;
  }

  .story-watch-btn {
    background: #10b981;
    color: white;
    padding: 1rem 2rem;
    font-weight: bold;
    transition: background-color 0.3s;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    font-size: 0.875rem;
  }

  .story-watch-btn:hover {
    background: #059669;
  }

  .section-heading {
    font-size: 3rem;
    font-weight: bold;
    text-align: center;
    margin-bottom: 4rem;
    font-family: monospace;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .about-panel {
    background: #1f2937;
    padding: 2rem;
    border-left: 4px solid #10b981;
  }

  .panel-title {
    color: #10b981;
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 1rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .panel-text {
    color: #d1d5db;
    font-size: 1.125rem;
    line-height: 1.6;
  }

  .privacy-icon {
    font-size: 2rem;
    margin-right: 1rem;
    color: #d97706;
  }

  .privacy-title {
    font-size: 1.25rem;
    font-weight: bold;
    color: #92400e;
    margin-bottom: 0.5rem;
  }

  .privacy-text {
    color: #a16207;
    line-height: 1.6;
  }
</style>