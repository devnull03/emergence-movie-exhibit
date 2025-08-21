<script lang="ts">
  import emergenceData from "$lib/content/films/emergence.json";
  import MetaHead from "$lib/components/MetaHead.svelte";
  import SubHeader from "$lib/components/SubHeader.svelte";
  import Section from "$lib/components/Section.svelte";
  import SubFooter from "$lib/components/SubFooter.svelte";
  import Alert from "$lib/components/Alert.svelte";
  import { Button } from "$lib/components/ui/button";
</script>

<MetaHead 
  title="Contact and Rights"
  description="Contact information and usage rights for Emergence: Out of the Shadows documentary materials"
  canonical="/contact"
/>

<SubHeader 
  pageTitle="Contact and Rights" 
  breadcrumbs={[{ label: "Contact and Rights" }]}
/>

<!-- Rights Notice -->
<Section>
  <Alert 
    type="warning" 
    message={emergenceData.rights.notice}
  />
</Section>

<!-- Contact Information -->
<Section title="Contact Information">
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
    <!-- Film Rights and Distribution -->
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <div class="flex items-center mb-4">
        <svg class="h-6 w-6 text-emerald-600 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
        </svg>
        <h3 class="text-lg font-semibold text-gray-900">Film Rights & Distribution</h3>
      </div>
      
      <p class="text-gray-600 mb-4">
        For screening rights, distribution inquiries, or licensing of documentary materials.
      </p>
      
      <div class="space-y-3 text-sm">
        <div>
          <dt class="font-medium text-gray-700">Email:</dt>
          <dd class="text-emerald-600">
            <a href="mailto:{emergenceData.rights.contactEmail}" class="hover:text-emerald-700">
              {emergenceData.rights.contactEmail}
            </a>
          </dd>
        </div>
        <div>
          <dt class="font-medium text-gray-700">Response Time:</dt>
          <dd class="text-gray-600">1-2 business days</dd>
        </div>
      </div>
      
      <div class="mt-4">
        <Button variant="outline" class="w-full">
          <a href="mailto:{emergenceData.rights.contactEmail}" class="no-underline">
            Send Inquiry
          </a>
        </Button>
      </div>
    </div>
    
    <!-- Educational Use -->
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <div class="flex items-center mb-4">
        <svg class="h-6 w-6 text-emerald-600 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253" />
        </svg>
        <h3 class="text-lg font-semibold text-gray-900">Educational Use</h3>
      </div>
      
      <p class="text-gray-600 mb-4">
        For classroom screenings, educational workshops, and academic research purposes.
      </p>
      
      <div class="space-y-3 text-sm mb-4">
        <p class="text-gray-600">
          Educational institutions may request screening permissions for non-commercial, 
          educational purposes. A teacher's discussion guide is available.
        </p>
      </div>
      
      <div class="flex gap-3">
        <Button variant="outline" size="sm" class="flex-1">
          <a href="mailto:{emergenceData.rights.contactEmail}?subject=Educational Screening Request" class="no-underline">
            Request Permission
          </a>
        </Button>
        <Button variant="outline" size="sm" class="flex-1">
          <a href={emergenceData.teacherGuide.href} target="_blank" rel="noopener noreferrer" class="no-underline">
            Get Guide
          </a>
        </Button>
      </div>
    </div>
  </div>
</Section>

<!-- Usage Guidelines -->
<Section title="Usage Guidelines" className="bg-gray-50">
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
    <!-- Permitted Uses -->
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">✅ Permitted Uses</h3>
      <ul class="space-y-2 text-sm text-gray-600">
        <li>• Personal viewing and reflection</li>
        <li>• Educational discussion and analysis</li>
        <li>• Academic research and citation</li>
        <li>• Community screenings with prior approval</li>
        <li>• Press coverage with proper attribution</li>
        <li>• Social media sharing of official clips/trailers</li>
      </ul>
      
      <div class="mt-4 p-3 bg-green-50 rounded-lg">
        <p class="text-xs text-green-800">
          <strong>Note:</strong> Educational institutions and non-profit organizations 
          are encouraged to contact us for screening permissions.
        </p>
      </div>
    </div>
    
    <!-- Prohibited Uses -->
    <div class="bg-white rounded-lg border border-gray-200 p-6">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">❌ Prohibited Uses</h3>
      <ul class="space-y-2 text-sm text-gray-600">
        <li>• Commercial distribution without license</li>
        <li>• Modification or editing of content</li>
        <li>• Public broadcasting without permission</li>
        <li>• Reproduction of full-length versions</li>
        <li>• Use in promotional materials without consent</li>
        <li>• Third-party monetization or advertising</li>
      </ul>
      
      <div class="mt-4 p-3 bg-red-50 rounded-lg">
        <p class="text-xs text-red-800">
          <strong>Warning:</strong> Unauthorized use may result in legal action. 
          Always contact us before any commercial or public use.
        </p>
      </div>
    </div>
  </div>
</Section>

<!-- Press and Media -->
<Section title="Press and Media">
  <div class="bg-white rounded-lg border border-gray-200 p-6">
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
      <div>
        <h3 class="text-lg font-semibold text-gray-900 mb-4">Press Inquiries</h3>
        <p class="text-gray-600 mb-4">
          Media professionals may request press materials, high-resolution images, 
          and interview opportunities.
        </p>
        
        <div class="space-y-2 text-sm">
          <p><strong>Available Materials:</strong></p>
          <ul class="text-gray-600 ml-4">
            <li>• Press kit and synopsis</li>
            <li>• High-resolution promotional images</li>
            <li>• Director and cast biographies</li>
            <li>• Awards and festival selection list</li>
            <li>• Video clips and trailers</li>
          </ul>
        </div>
      </div>
      
      <div>
        <h3 class="text-lg font-semibold text-gray-900 mb-4">Media Guidelines</h3>
        <ul class="space-y-2 text-sm text-gray-600">
          <li>• Always credit the full film title</li>
          <li>• Include director and production information</li>
          <li>• Use official promotional materials when available</li>
          <li>• Respect privacy of cast members</li>
          <li>• Contact for permission before extensive excerpts</li>
        </ul>
        
        <div class="mt-4">
          <Button variant="outline" size="sm">
            <a href="mailto:{emergenceData.rights.contactEmail}?subject=Press Inquiry" class="no-underline">
              Request Press Materials
            </a>
          </Button>
        </div>
      </div>
    </div>
  </div>
</Section>

<!-- Additional Resources -->
<Section className="bg-emerald-50">
  <div class="text-center max-w-2xl mx-auto">
    <h3 class="text-xl font-semibold text-gray-900 mb-4">Need More Information?</h3>
    <p class="text-gray-700 mb-6">
      Visit our official sources for comprehensive information about the documentary.
    </p>
    <div class="flex flex-col sm:flex-row gap-4 justify-center">
      <Button>
        <a href={emergenceData.sources.officialSite} target="_blank" rel="noopener noreferrer" class="text-white no-underline">
          Official Website
        </a>
      </Button>
      <Button variant="outline">
        <a href={emergenceData.sources.archiveListing} target="_blank" rel="noopener noreferrer" class="no-underline">
          Archive Entry
        </a>
      </Button>
      <Button variant="outline">
        <a href="/sources" class="no-underline">
          All Sources
        </a>
      </Button>
    </div>
  </div>
</Section>

<SubFooter />