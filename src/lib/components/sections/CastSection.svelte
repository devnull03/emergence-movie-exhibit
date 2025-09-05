<script lang="ts">
  import castData from "$lib/content/cast.json";
  import { User } from "@lucide/svelte";
  import SectionTitle from "../SectionTitle.svelte";

  interface CastMember {
    name: string;
    bio: string;
    photo: string | null;
    photo_credits?: string;
    position: string;
  }

  const castMembers: CastMember[] = castData.people;
  let selectedMember = $state(0);

  function selectMember(idx: number) {
    if (idx === selectedMember) return;
    selectedMember = idx;
  }
</script>

<section
  class="w-full h-screen text-black! flex flex-col items-center justify-center gap-4"
>
  <SectionTitle title="Cast & Crew" color="text-black" />

  <!-- Main Showcase Section -->
  <div class="h-[40%] flex items-center justify-center px-6">
    <div class="w-full max-w-4xl mx-auto grid md:grid-cols-5 items-center">
      <div class="overflow-hidden flex justify-center col-span-3">
        {#key selectedMember}
          {#if castMembers[selectedMember].photo}
            <img
              src={castMembers[selectedMember].photo}
              alt={castMembers[selectedMember].name}
              class="h-full object-cover aspect-video transition-transform duration-500 ease-out starting:scale-125"
            />
          {:else}
            <div
              class="h-full aspect-video bg-gray-200 flex items-center justify-center transition-transform duration-500 ease-out starting:scale-125"
            >
              <User class="w-16 h-16 text-gray-400" />
            </div>
          {/if}
        {/key}
      </div>

      <!-- {#key selectedMember} -->
      <div
        class="space-y-4 h-full flex flex-col justify-end col-span-2 ml-4 text-pretty transition-all duration-300 ease-out *:font-[Poppins] *:tracking-wider *:leading-tight"
      >
        <h2 class="text-lg">
          {castMembers[selectedMember].name}
        </h2>

        <p class="leading-relaxed text-xs">
          {castMembers[selectedMember].bio}
        </p>
      </div>
      <!-- {/key} -->
    </div>
  </div>

  <!-- Production Company Section -->
  <div class="text-center">
    <p class="text-sm text-gray-600">
      <span class="font-medium">Production Company –</span>
      <span class="font-semibold text-black">Sher Films</span>
      <span class="text-gray-500"
        >(A Division of the Sher Vancouver LGBTQ Friends Society)</span
      >
    </p>
  </div>

  <!-- Cast Grid Section -->
  <div class="max-w-6xl mx-auto h-[40%] flex flex-col justify-center">
    <div class="grid grid-cols-3 md:grid-cols-6 gap-3 max-w-4xl mx-auto">
      {#each castMembers as member, idx}
        <button
          onmouseenter={() => selectMember(idx)}
          onclick={() => selectMember(idx)}
          class="group relative aspect-square rounded-xl overflow-hidden bg-gray-800"
        >
          {#if member.photo}
            <img
              src={member.photo}
              alt={member.name}
              class="w-full h-full object-cover"
            />
          {:else}
            <div
              class="w-full h-full bg-gray-200 flex items-center justify-center"
            >
              <User class="w-8 h-8 text-gray-400" />
            </div>
          {/if}

          <!-- Single overlay for both cases -->
          <div
            class="absolute inset-0 bg-black/40 backdrop-blur backdrop-sepia-65 flex items-end justify-end *:text-right p-2 transition-opacity duration-300 group-hover:opacity-0"
          >
            <p
              class="text-2xl font-bold text-gray-100 drop-shadow-lg font-[Bebas_Neue] uppercase leading-none"
            >
              {member.name}
            </p>
          </div>
        </button>
      {/each}
    </div>
  </div>
</section>
