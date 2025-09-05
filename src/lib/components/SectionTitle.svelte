<script lang="ts">
  interface Props {
    title: string;
    color?: string;
  }

  let { title, color = "text-black" }: Props = $props();
</script>

<div
  class="absolute left-0 top-0 h-screen flex items-end justify-center z-10"
  style="writing-mode: vertical-rl; text-orientation: mixed;"
>
  <h1
    class="font-bold uppercase tracking-widest leading-tight font-[Bebas_Neue] {color} rotate-180"
    style="font-size: min(12vw, calc(100vh / {title.length}));"
  >
    {title}
  </h1>
</div>
