<script lang="ts">
  import type { Snippet } from "svelte";

  interface Props {
    children?: Snippet;
    class?: string;
    hasRoundedTop?: boolean;
  }

  let {
    children,
    class: className = "",
    hasRoundedTop = true,
  }: Props = $props();

  let isAtTop = $state(false);
  let sectionElement: HTMLDivElement;

  $effect(() => {
    if (!sectionElement || !hasRoundedTop) return;

    const observer = new IntersectionObserver(
      ([entry]) => {
        // When the section reaches the top of the viewport
        isAtTop = entry.boundingClientRect.top <= 0 && entry.isIntersecting;
      },
      {
        threshold: [0, 1],
        rootMargin: "0px",
      }
    );

    observer.observe(sectionElement);

    return () => {
      observer.disconnect();
    };
  });
</script>

<div
  bind:this={sectionElement}
  class="pl-[12vw] {className}"
  class:rounded-t-2xl={hasRoundedTop && !isAtTop}
>
  <div class="max-w-5xl md:max-w-6xl mx-auto w-full px-[4vw] md:px-[3vw]">
    {@render children?.()}
  </div>
</div>
