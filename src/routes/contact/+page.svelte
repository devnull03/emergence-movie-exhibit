<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
</script>

<svelte:head>
  <title>Contact & Rights - Emergence: Out of the Shadows</title>
  <meta name="description" content="Contact information and usage rights for Emergence: Out of the Shadows documentary materials" />
</svelte:head>

<main class="bg-gray-100">
  <!-- Hero Section -->
  <section class="bg-black text-white relative overflow-hidden">
    <div class="absolute inset-0" style="background: linear-gradient(135deg, #225c9e 0%, #0ea568 100%);"></div>
    <div class="absolute inset-0 bg-black opacity-60"></div>
    
    <div class="relative z-10 max-w-6xl mx-auto px-8 py-24 text-center">
      <h1 class="text-5xl md:text-7xl font-mono font-bold mb-8 leading-tight">
        CONTACT &<br>RIGHTS
      </h1>
      <p class="text-xl md:text-2xl mb-12 max-w-3xl mx-auto leading-relaxed">
        Information for screening, distribution, educational use, and media inquiries
      </p>
      
      <!-- Rights Warning -->
      <div class="bg-amber-500 text-black p-6 max-w-4xl mx-auto">
        <h2 class="text-lg font-bold mb-2">⚠ IMPORTANT USAGE NOTICE</h2>
        <p class="font-semibold">
          {emergenceData.rights.notice}
        </p>
      </div>
    </div>
  </section>

  <!-- Primary Contact -->
  <section class="py-20">
    <div class="max-w-6xl mx-auto px-8">
      <h2 class="section-heading">Primary Contact</h2>
      
      <div class="contact-card-large">
        <div class="contact-header">
          <div class="contact-icon">📧</div>
          <div>
            <h3 class="contact-title">Film Rights & Distribution</h3>
            <p class="contact-subtitle">For all screening, distribution, and licensing inquiries</p>
          </div>
        </div>
        
        <div class="contact-details">
          <div class="contact-email">
            <a href="mailto:{emergenceData.rights.contactEmail}">
              {emergenceData.rights.contactEmail}
            </a>
          </div>
          <div class="contact-note">Response within 1-2 business days</div>
        </div>
        
        <div class="contact-actions">
          <a href="mailto:{emergenceData.rights.contactEmail}" class="contact-btn primary">
            Send General Inquiry
          </a>
          <a href="mailto:{emergenceData.rights.contactEmail}?subject=Educational Screening Request" class="contact-btn secondary">
            Educational Screening Request
          </a>
        </div>
      </div>
    </div>
  </section>

  <!-- Usage Types -->
  <section class="bg-white py-20">
    <div class="max-w-7xl mx-auto px-8">
      <h2 class="section-heading">Usage Categories</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <!-- Educational -->
        <div class="usage-card">
          <div class="usage-icon">🎓</div>
          <h3 class="usage-title">Educational Use</h3>
          <ul class="usage-list">
            <li>Classroom screenings</li>
            <li>Academic workshops</li>
            <li>Student research</li>
            <li>Discussion groups</li>
          </ul>
          <div class="usage-action">
            <a href={emergenceData.teacherGuide.href} target="_blank" class="usage-btn">Download Teaching Guide</a>
          </div>
        </div>
        
        <!-- Media -->
        <div class="usage-card">
          <div class="usage-icon">📺</div>
          <h3 class="usage-title">Press & Media</h3>
          <ul class="usage-list">
            <li>Press coverage</li>
            <li>Interview requests</li>
            <li>Promotional materials</li>
            <li>Festival submissions</li>
          </ul>
          <div class="usage-action">
            <a href="mailto:{emergenceData.rights.contactEmail}?subject=Press Inquiry" class="usage-btn">Request Press Kit</a>
          </div>
        </div>
        
        <!-- Community -->
        <div class="usage-card">
          <div class="usage-icon">👥</div>
          <h3 class="usage-title">Community Screenings</h3>
          <ul class="usage-list">
            <li>Non-profit events</li>
            <li>Community centers</li>
            <li>Awareness campaigns</li>
            <li>Support groups</li>
          </ul>
          <div class="usage-action">
            <a href="mailto:{emergenceData.rights.contactEmail}?subject=Community Screening Request" class="usage-btn">Request Permission</a>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Legal Guidelines -->
  <section class="bg-black text-white py-20">
    <div class="max-w-6xl mx-auto px-8">
      <h2 class="section-heading text-white">Legal Guidelines</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
        <div class="legal-panel permitted">
          <h3 class="legal-title">✅ PERMITTED</h3>
          <ul class="legal-list">
            <li>Personal viewing</li>
            <li>Educational analysis</li>
            <li>Academic citation</li>
            <li>Community screenings (with approval)</li>
            <li>Press coverage (with attribution)</li>
            <li>Sharing official trailers</li>
          </ul>
        </div>
        
        <div class="legal-panel prohibited">
          <h3 class="legal-title">❌ PROHIBITED</h3>
          <ul class="legal-list">
            <li>Commercial distribution</li>
            <li>Content modification</li>
            <li>Public broadcast (without permission)</li>
            <li>Full-length reproduction</li>
            <li>Unauthorized monetization</li>
            <li>Third-party advertising</li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <!-- Resources -->
  <section class="bg-emerald-600 text-white py-20">
    <div class="max-w-4xl mx-auto text-center px-8">
      <h2 class="text-4xl font-bold mb-8">Additional Resources</h2>
      <p class="text-xl mb-12">
        Visit our official channels for more comprehensive information.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <a href="https://emergencefilm.net/" 
           target="_blank" 
           rel="noopener noreferrer"
           class="bg-white text-emerald-600 px-8 py-4 font-bold hover:bg-gray-100 transition-colors">
          Official Website →
        </a>
        <a href="https://sacda.ca" 
           target="_blank" 
           rel="noopener noreferrer"
           class="border-2 border-white text-white hover:bg-white hover:text-emerald-600 px-8 py-4 font-bold transition-colors">
          SACDA Archive →
        </a>
      </div>
    </div>
  </section>
</main>

<style>
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

  .contact-card-large {
    background: white;
    border: 3px solid #10b981;
    max-width: 4xl;
    margin: 0 auto;
    overflow: hidden;
  }

  .contact-header {
    background: #f0fdf4;
    padding: 2rem;
    display: flex;
    align-items: center;
    gap: 1.5rem;
    border-bottom: 2px solid #10b981;
  }

  .contact-icon {
    font-size: 3rem;
  }

  .contact-title {
    font-size: 2rem;
    font-weight: bold;
    color: #1f2937;
    font-family: monospace;
  }

  .contact-subtitle {
    color: #6b7280;
    font-size: 1.125rem;
    margin-top: 0.5rem;
  }

  .contact-details {
    padding: 2rem;
    text-align: center;
  }

  .contact-email {
    font-size: 2rem;
    font-weight: bold;
    color: #10b981;
    font-family: monospace;
    margin-bottom: 1rem;
  }

  .contact-email a {
    color: inherit;
    text-decoration: none;
  }

  .contact-email a:hover {
    color: #059669;
  }

  .contact-note {
    color: #6b7280;
    font-size: 0.875rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .contact-actions {
    padding: 2rem;
    background: #f8fafc;
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    justify-content: center;
  }

  .contact-btn {
    padding: 1rem 2rem;
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    font-size: 0.875rem;
    transition: all 0.3s;
    text-decoration: none;
  }

  .contact-btn.primary {
    background: #10b981;
    color: white;
  }

  .contact-btn.primary:hover {
    background: #059669;
  }

  .contact-btn.secondary {
    background: transparent;
    color: #10b981;
    border: 2px solid #10b981;
  }

  .contact-btn.secondary:hover {
    background: #10b981;
    color: white;
  }

  .usage-card {
    background: white;
    border: 2px solid #d1d5db;
    padding: 2rem;
    text-align: center;
    transition: border-color 0.3s;
  }

  .usage-card:hover {
    border-color: #10b981;
  }

  .usage-icon {
    font-size: 3rem;
    margin-bottom: 1rem;
  }

  .usage-title {
    font-size: 1.5rem;
    font-weight: bold;
    color: #1f2937;
    margin-bottom: 1rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .usage-list {
    list-style: none;
    padding: 0;
    margin-bottom: 2rem;
  }

  .usage-list li {
    color: #6b7280;
    margin-bottom: 0.5rem;
    position: relative;
    padding-left: 1rem;
  }

  .usage-list li:before {
    content: "•";
    color: #10b981;
    position: absolute;
    left: 0;
  }

  .usage-btn {
    background: #10b981;
    color: white;
    padding: 0.75rem 1.5rem;
    font-weight: bold;
    font-size: 0.875rem;
    text-decoration: none;
    transition: background-color 0.3s;
  }

  .usage-btn:hover {
    background: #059669;
  }

  .legal-panel {
    padding: 2rem;
    border-left: 4px solid;
  }

  .legal-panel.permitted {
    background: #064e3b;
    border-left-color: #10b981;
  }

  .legal-panel.prohibited {
    background: #7f1d1d;
    border-left-color: #ef4444;
  }

  .legal-title {
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 1.5rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .legal-list {
    list-style: none;
    padding: 0;
  }

  .legal-list li {
    color: #d1d5db;
    margin-bottom: 0.75rem;
    position: relative;
    padding-left: 1rem;
  }

  .legal-list li:before {
    content: "•";
    position: absolute;
    left: 0;
  }

  .legal-panel.permitted .legal-list li:before {
    color: #10b981;
  }

  .legal-panel.prohibited .legal-list li:before {
    color: #ef4444;
  }
</style>