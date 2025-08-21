<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
</script>

<svelte:head>
  <title>Awards & Recognition - Emergence: Out of the Shadows</title>
  <meta name="description" content="51 international festival selections, 7 awards, and recognition at Academy Award, BAFTA, and Canadian Screen Award qualifying festivals." />
</svelte:head>

<main class="bg-gray-100">
  <!-- Hero Banner -->
  <section class="bg-black text-white min-h-screen flex items-center justify-center relative overflow-hidden">
    <!-- Background gradient -->
    <div class="absolute inset-0" style="background: linear-gradient(135deg, #0ea568 0%, #5b2d83 50%, #225c9e 100%);"></div>
    <div class="absolute inset-0 bg-black opacity-60"></div>
    
    <div class="relative z-10 text-center max-w-6xl mx-auto px-8">
      <!-- Hero Stats Panel -->
      <div class="bg-black bg-opacity-80 p-16 mb-12 exhibit-panel">
        <h1 class="text-6xl md:text-8xl font-mono font-bold mb-8 leading-none">
          AWARDS &<br>RECOGNITION
        </h1>
        
        <!-- Main Stats Grid -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-12">
          <div class="hero-stat">
            <div class="hero-stat-number">{emergenceData.awardsSummary.countsByResult.totalOfficialSelections}</div>
            <div class="hero-stat-label">Festival Selections</div>
          </div>
          <div class="hero-stat">
            <div class="hero-stat-number">{emergenceData.awardsSummary.countsByResult.awardWinner}</div>
            <div class="hero-stat-label">Award Wins</div>
          </div>
          <div class="hero-stat">
            <div class="hero-stat-number">{emergenceData.awardsSummary.countsByResult.finalist}</div>
            <div class="hero-stat-label">Finalists</div>
          </div>
          <div class="hero-stat">
            <div class="hero-stat-number">{emergenceData.awardsSummary.countsByResult.closingFilm + emergenceData.awardsSummary.countsByResult.openingFilm}</div>
            <div class="hero-stat-label">Special Screenings</div>
          </div>
        </div>
        
        <p class="text-xl md:text-2xl mb-8 max-w-3xl mx-auto leading-relaxed">
          International recognition spanning LGBTQ+, South Asian, and documentary film festivals worldwide
        </p>
        
        <!-- Qualifying Festival Badges -->
        <div class="flex flex-wrap justify-center gap-4">
          <div class="qualifying-badge">Academy Award Qualifying</div>
          <div class="qualifying-badge">BAFTA Qualifying</div>
          <div class="qualifying-badge">Canadian Screen Award Qualifying</div>
        </div>
      </div>
    </div>
  </section>

  <!-- Festival Categories -->
  <section class="festival-categories">
    <div class="max-w-7xl mx-auto px-8 py-20">
      <h2 class="section-heading">Festival Categories</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        <div class="category-card">
          <div class="category-number">{emergenceData.awardsSummary.countsByFestivalType.lgbtq}</div>
          <div class="category-name">LGBTQ+ Festivals</div>
        </div>
        <div class="category-card">
          <div class="category-number">{emergenceData.awardsSummary.countsByFestivalType.southAsian}</div>
          <div class="category-name">South Asian Festivals</div>
        </div>
        <div class="category-card">
          <div class="category-number">{emergenceData.awardsSummary.countsByFestivalType.documentary}</div>
          <div class="category-name">Documentary Festivals</div>
        </div>
        <div class="category-card">
          <div class="category-number">{emergenceData.awardsSummary.countsByFestivalType.international}</div>
          <div class="category-name">International Festivals</div>
        </div>
      </div>
    </div>
  </section>

  <!-- Award Highlights -->
  <section class="bg-black text-white">
    <div class="max-w-7xl mx-auto px-8 py-20">
      <h2 class="section-heading text-white">Major Recognition</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        {#each emergenceData.awardsHighlights as award}
          <div class="award-highlight-card">
            <div class="award-type">{award.result}</div>
            <div class="award-title">{award.title}</div>
            <div class="award-festival">{award.festival}</div>
            <div class="award-date">{new Date(award.date).getFullYear()}</div>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- Notable Festivals -->
  <section class="notable-festivals">
    <div class="max-w-7xl mx-auto px-8 py-20">
      <h2 class="section-heading">Notable Festival Selections</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        {#each emergenceData.awardsSummary.otherMajorSelections as festival}
          <div class="festival-badge">
            {festival}
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- Call to Action -->
  <section class="bg-emerald-600 text-white">
    <div class="max-w-4xl mx-auto text-center px-8 py-20">
      <h2 class="text-4xl font-bold mb-8">Experience the Film</h2>
      <p class="text-xl mb-12">
        See why festival programmers and audiences worldwide have embraced this powerful documentary.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <a href="/" class="bg-white text-emerald-600 px-8 py-4 font-bold hover:bg-gray-100 transition-colors">
          Watch Film
        </a>
        <a href="/cast" class="border-2 border-white text-white hover:bg-white hover:text-emerald-600 px-8 py-4 font-bold transition-colors">
          Meet the Cast
        </a>
      </div>
    </div>
  </section>
</main>

<style>
  .exhibit-panel {
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
  }

  .hero-stat {
    text-align: center;
  }

  .hero-stat-number {
    font-size: 4rem;
    font-weight: bold;
    color: #10b981;
    font-family: monospace;
    line-height: 1;
  }

  .hero-stat-label {
    font-size: 0.875rem;
    color: #d1d5db;
    margin-top: 0.5rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .qualifying-badge {
    background: #10b981;
    color: white;
    padding: 0.75rem 1.5rem;
    font-weight: bold;
    font-size: 0.875rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .section-heading {
    font-size: 3rem;
    font-weight: bold;
    text-align: center;
    margin-bottom: 4rem;
    color: #1f2937;
    font-family: monospace;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .festival-categories {
    background: #f8fafc;
  }

  .category-card {
    background: white;
    border: 2px solid #10b981;
    padding: 2rem;
    text-align: center;
    transition: transform 0.3s ease;
  }

  .category-card:hover {
    transform: translateY(-4px);
  }

  .category-number {
    font-size: 3rem;
    font-weight: bold;
    color: #10b981;
    font-family: monospace;
    line-height: 1;
  }

  .category-name {
    font-size: 1rem;
    color: #374151;
    margin-top: 1rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .award-highlight-card {
    background: #1f2937;
    padding: 1.5rem;
    border-left: 4px solid #10b981;
  }

  .award-type {
    color: #10b981;
    font-weight: bold;
    font-size: 0.875rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-bottom: 0.5rem;
  }

  .award-title {
    color: white;
    font-weight: bold;
    font-size: 1.125rem;
    margin-bottom: 0.5rem;
  }

  .award-festival {
    color: #9ca3af;
    font-size: 0.875rem;
    margin-bottom: 0.5rem;
  }

  .award-date {
    color: #6b7280;
    font-size: 0.75rem;
    font-family: monospace;
  }

  .notable-festivals {
    background: #f8fafc;
  }

  .festival-badge {
    background: white;
    border: 1px solid #d1d5db;
    padding: 1rem;
    text-align: center;
    font-weight: 500;
    color: #374151;
    transition: border-color 0.3s ease;
  }

  .festival-badge:hover {
    border-color: #10b981;
  }
</style>