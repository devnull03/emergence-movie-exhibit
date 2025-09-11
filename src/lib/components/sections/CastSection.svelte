<script lang="ts">
  import castData from "$lib/content/cast.json";
  import { User } from "@lucide/svelte";
  import SectionTitle from "../SectionTitle.svelte";
  import Section from "../Section.svelte";

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

<Section
  class="w-full h-screen text-background! flex flex-col items-center justify-center gap-4 bg-gray-900"
>
  <SectionTitle title="Cast & Crew" color="text-background" />

  <!-- Main Showcase Section -->
  <div
    class="h-[30%] sm:h-[35%] md:h-[40%] flex items-center justify-center px-4 sm:px-6"
  >
    <div
      class="w-full max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-5 gap-4 items-center"
    >
      <div class="overflow-hidden flex justify-center md:col-span-3">
        {#key selectedMember}
          {#if castMembers[selectedMember].photo}
            <img
              src={castMembers[selectedMember].photo}
              alt={castMembers[selectedMember].name}
              class="w-full h-48 sm:h-56 md:h-64 lg:h-72 object-cover aspect-video transition-transform duration-500 ease-out starting:scale-125"
            />
          {:else}
            <div
              class="w-full h-48 sm:h-56 md:h-64 lg:h-72 aspect-video bg-gray-200 flex items-center justify-center transition-transform duration-500 ease-out starting:scale-125"
            >
              <User
                class="w-12 h-12 sm:w-14 sm:h-14 md:w-16 md:h-16 text-gray-400"
              />
            </div>
          {/if}
        {/key}
      </div>

      <!-- {#key selectedMember} -->
      <div
        class="space-y-2 sm:space-y-3 md:space-y-4 h-full flex flex-col justify-end md:col-span-2 ml-2 sm:ml-3 md:ml-4 text-pretty transition-all duration-300 ease-out *:font-[Poppins] *:tracking-wider *:leading-tight"
      >
        <h2 class="text-base sm:text-lg md:text-xl">
          {castMembers[selectedMember].name}
        </h2>

        <p class="leading-relaxed text-xs sm:text-sm">
          {castMembers[selectedMember].bio}
        </p>
      </div>
      <!-- {/key} -->
    </div>
  </div>

  <!-- Production Company Section -->
  <!-- <div class="text-center"> -->
  <p class="text-xs sm:text-sm text-background text-center px-4">
    <span class="font-medium">Production Company –</span>
    <span class="font-semibold text-white">Sher Films</span>
    <span class=""
      >(A Division of the Sher Vancouver LGBTQ Friends Society)</span
    >
  </p>
  <!-- </div> -->

  <!-- Cast Grid Section -->
  <div
    class="max-w-6xl mx-auto h-[30%] sm:h-[35%] md:h-[40%] flex flex-col justify-center pt-4 sm:pt-6 px-4"
  >
    <div
      class="grid grid-cols-5 gap-2 sm:gap-3 max-w-4xl mx-auto"
    >
      {#each castMembers as member, idx}
        <button
          onmouseenter={() => selectMember(idx)}
          onclick={() => selectMember(idx)}
          class="group relative w-full aspect-square rounded-lg sm:rounded-xl overflow-hidden bg-gray-800"
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
              <User class="w-6 h-6 sm:w-7 sm:h-7 md:w-8 md:h-8 text-gray-400" />
            </div>
          {/if}

          <!-- Single overlay for both cases -->
          <div
            class="absolute inset-0 bg-black/40 backdrop-blur backdrop-sepia-65 flex items-end justify-end *:text-right p-1 sm:p-2 transition-opacity duration-300 group-hover:opacity-0"
          >
            <p
              class="text-xs sm:text-sm md:text-lg lg:text-xl xl:text-2xl font-bold text-gray-100 drop-shadow-lg font-[Bebas_Neue] uppercase leading-none"
            >
              {member.name}
            </p>
          </div>
        </button>
      {/each}
    </div>
  </div>
</Section>
