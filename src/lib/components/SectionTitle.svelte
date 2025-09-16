<script lang="ts">
  interface Props {
    title: string;
    color?: string;
    class?: string;
  }

  let { title, color = "text-black", class: className = "" }: Props = $props();
</script>

<div
  class="absolute left-0 top-0 h-screen flex items-end justify-center z-10 {className}"
  style="writing-mode: vertical-rl; text-orientation: mixed;"
>
  <h1
    class="font-bold uppercase tracking-widest leading-tight font-[Bebas_Neue] {color} rotate-180"
    style="font-size: clamp(3rem, 8vw, 6rem);"
  >
    {title}
  </h1>
</div>
