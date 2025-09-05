<script lang="ts">
  import { onMount, onDestroy } from "svelte";
  import { browser } from "$app/environment";
  import { gsap } from "gsap";
  import logo from "$lib/assets/logo.png";

  let lastScrollY = $state(0);
  let isHidden = $state(false);
  let tween: gsap.core.Tween | undefined;

  const navigationItems = [
    { label: "Home", href: "/" },
    { label: "Awards", href: "#awards" },
    { label: "Cast & Crew", href: "#cast" },
    { label: "Sources", href: "#sources" },
  ];

  function handleScroll() {
    if (!browser) return;

    const currentScrollY = window.scrollY;

    const headerHeight = 100;
    const delayVh = window.innerHeight * 0.4;
    const hideThreshold = headerHeight + delayVh;

    if (currentScrollY <= hideThreshold) {
      if (isHidden) {
        showHeader();
      }
      lastScrollY = currentScrollY;
      return;
    }

    const scrollingDown = currentScrollY > lastScrollY;
    const scrollingUp = currentScrollY < lastScrollY;

    if (Math.abs(currentScrollY - lastScrollY) > 5) {
      if (scrollingDown && !isHidden) {
        hideHeader();
      } else if (scrollingUp && isHidden) {
        showHeader();
      }
    }

    lastScrollY = currentScrollY;
  }

  function hideHeader() {
    if (isHidden) return;

    if (tween) tween.kill();

    isHidden = true;
    tween = gsap.to("#subheader", {
      y: "-100%",
      duration: 0.3,
      ease: "power2.out",
    });
  }

  function showHeader() {
    if (!isHidden) return;

    if (tween) tween.kill();

    isHidden = false;
    tween = gsap.to("#subheader", {
      y: "0%",
      duration: 0.4,
      ease: "power2.out",
    });
  }

  onMount(() => {
    if (browser) {
      window.addEventListener("scroll", handleScroll, { passive: true });
    }
  });

  onDestroy(() => {
    if (browser) {
      window.removeEventListener("scroll", handleScroll);
    }
    if (tween) tween.kill();
  });
</script>

<div id="subheader" class="sticky top-0 w-full z-40 -mt-2">
  <div class="flex items-center justify-between w-full px-8 py-2">
    <!-- Left Section: Film Credit -->
    <div class="flex-1 flex justify-start">
      <div
        class="text-white font-[Bebas_Neue] text-sm md:text-lg tracking-wide uppercase font-semibold select-none flex items-center gap-2"
      >
        A FILM BY VINAY GIRIDHAR
      </div>
    </div>

    <!-- Middle Section: Logo -->
    <div class="flex-1 flex justify-center">
      <img src={logo} alt="Logo" class="h-8 md:h-12 w-auto object-contain" />
    </div>

    <!-- Right Section: Navigation Menu -->
    <div class="flex-1 flex justify-end">
      <nav class="flex items-center gap-3">
        {#each navigationItems as item}
          <div class="flex flex-col items-center overflow-hidden">
            <a
              href={item.href}
              class="group text-xs md:text-sm tracking-tight font-[Poppins] text-white uppercase transition-all duration-200 w-full"
            >
              <span class="block">{item.label}</span>
              <span
                class="block h-0.5 bg-white rounded transition-all duration-200 ease-in-out w-0 group-hover:w-full"
              ></span>
            </a>
          </div>
        {/each}
      </nav>
    </div>
  </div>
</div>
