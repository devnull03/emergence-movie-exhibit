<script lang="ts">
  import { onMount } from "svelte";

  interface CastMember {
    name: string;
    bio: string;
    photo: string;
    youtubeId?: string;
    runtime?: string;
  }

  // Cast data with available photos and accurate bios from website
  const castMembers: CastMember[] = [
    {
      name: "Kayden",
      bio: "Kayden is a mid-twenties Punjabi Sikh gay man from Punjab, India. The film explores his survival, resilience, resourcefulness, and ability to overcome barriers despite the trauma of family rejection and the impact this had on his psychological health. Kayden tells a poignant story of self-discovery while embracing his newfound family and life.",
      photo: "/src/lib/assets/stills/Kayden Still Photo (1).jpg",
      youtubeId: "7CGVn6f0r-c",
      runtime: "28:04",
    },
    {
      name: "Jag",
      bio: "Jag is a queer Punjabi artist. She and her wife, Agata, have been together for 8 years and together they have two beautiful children. In the film, she discusses the challenges she faced coming out to her parents, and how her life changed when she met Agata.",
      photo: "/src/lib/assets/stills/Rajwant and Jag Still Photo (1).jpg",
      youtubeId: "sphBx4biw6g",
      runtime: "29:46",
    },
    {
      name: "Alex (Amar)",
      bio: "Amar is a late forties gay Punjabi Sikh man from suburban Vancouver. He speaks about his coming out journey and the reactions of his parents, including the disapproval he got from certain segments of the broader Punjabi Sikh community, when he came out publicly as a gay Sikh. Amar is the Founder of Sher Vancouver, a non-profit for queer South Asians and friends.",
      photo: "/src/lib/assets/stills/Alex Still Photo (1).jpg",
      youtubeId: "e7FEMIXuoGw",
      runtime: "25:01",
    },
    {
      name: "Jaspal",
      bio: "Jaspal is the caring and compassionate mother of Alex. She explains the struggle she experienced trying to come to terms with her son's sexuality. Jaspal worked as a nurses aide for many years, and raised three boys largely as a single parent. She shares her authentic self and her courage to share her true feelings around her son being gay and how she tried to reconcile it with her Sikh faith.",
      photo: "/src/lib/assets/stills/Jaspal Still Photo (1).jpg",
    },
    {
      name: "Rajwant & Avtar",
      bio: "Rajwant is Jag's wonderful mother who provides the voice of the traditional Punjabi Sikh mother. Avtar is Jag's kind-hearted father who immigrated to Canada in 1972. Since finding out that both of their children are gay, they have spent years being advocates for the LGBTQ+ community and have helped break down barriers in the South Asian community.",
      photo: "/src/lib/assets/stills/Avtar and Rajwant Still Photo (1) (1).jpg",
    },
  ];

  let selectedMember = $state(0);

  function selectMember(idx: number) {
    if (idx === selectedMember) return;
    selectedMember = idx;
  }
</script>

<section
  class="w-full h-screen bg-white text-black! flex flex-col items-center justify-center"
>
  <!-- Main Showcase Section -->
  <div class="h-[40%] flex items-center justify-center px-6">
    <div class="w-full max-w-4xl mx-auto grid md:grid-cols-5 items-center">
      <div class="overflow-hidden flex justify-center col-span-3">
        {#key selectedMember}
          <img
            src={castMembers[selectedMember].photo}
            alt={castMembers[selectedMember].name}
            class="h-full object-cover aspect-video transition-transform duration-300 ease-out starting:scale-110"
          />
        {/key}
      </div>

      <!-- Cast Member Info -->
      <div
        class="space-y-4 h-full flex flex-col justify-end col-span-2 ml-4 text-pretty transition-all duration-300 ease-out"
      >
        <h2 class="text-lg">
          {castMembers[selectedMember].name}
        </h2>

        <p class="leading-relaxed text-xs">
          {castMembers[selectedMember].bio}
        </p>
      </div>
    </div>
  </div>

  <!-- Cast Grid Section -->
  <div class="max-w-6xl mx-auto h-[40%] flex flex-col justify-center">
    <h3 class="text-xl font-semibold mb-4 text-center text-white">
      Featured Cast
    </h3>

    <div class="grid grid-cols-2 md:grid-cols-5 gap-3 max-w-4xl mx-auto">
      {#each castMembers as member, idx}
        <button
          onmouseenter={() => selectMember(idx)}
          onclick={() => selectMember(idx)}
          class="group relative aspect-square rounded-xl overflow-hidden bg-gray-800 transition-all duration-300 hover:scale-105"
        >
          <img
            src={member.photo}
            alt={member.name}
            class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-110"
          />

          <!-- Overlay with name -->
          <div
            class="absolute inset-0 bg-black bg-opacity-0 group-hover:bg-opacity-40 transition-all duration-300 flex items-end"
          >
            <div
              class="p-2 text-white opacity-0 group-hover:opacity-100 transition-opacity duration-300"
            >
              <p class="text-xs font-medium">{member.name}</p>
            </div>
          </div>

          <!-- Active indicator -->
          {#if idx === selectedMember}
            <div
              class="absolute inset-0 bg-black bg-opacity-10 pointer-events-none"
            ></div>
          {/if}
        </button>
      {/each}
    </div>
  </div>
</section>
