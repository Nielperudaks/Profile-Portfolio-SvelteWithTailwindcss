<script lang="ts">
  import { cn } from "$lib/utils/cn"
  import { AnimatePresence, Motion } from "svelte-motion";
  import { onMount } from "svelte";

  let { 
    class: className = "", 
    words = ["Gradual Spacing"], 
    duration = 0.5, 
    delayMultiple = 0.04, 
    cycleDuration = 2000,
    framerProps = {
      hidden: { opacity: 0, x: -20 },
      visible: { opacity: 1, x: 0 },
      exit: { opacity: 0, x: 20 },
    }
  } = $props();

  let currentWordIndex = $state(0);
  let isAnimatingOut = $state(false);
  let showWord = $state(true);
  
  // Derived values using runes syntax
  const currentWord = $derived(words[currentWordIndex]);
  const wordsSplit = $derived(currentWord.split(""));

  onMount(() => {
    if (words.length <= 1) return;

    const cycle = () => {
      // Wait for the specified duration, then start out animation
      setTimeout(() => {
        isAnimatingOut = true;
        
        // After out animation completes, hide word and switch to next
        setTimeout(() => {
          showWord = false;
          currentWordIndex = (currentWordIndex + 1) % words.length;
          
          // Immediately show next word and reset animation state
          setTimeout(() => {
            showWord = true;
            isAnimatingOut = false;
          }, 50); // Small delay to ensure clean transition
        }, (wordsSplit.length * delayMultiple + duration) * 1000);
      }, cycleDuration);
    };

    // Start the first cycle
    cycle();
    
    // Set up interval for continuous cycling
    const interval = setInterval(cycle, cycleDuration + (wordsSplit.length * delayMultiple + duration) * 1000 + 50);

    return () => clearInterval(interval);
  });
</script>

<!-- Added overflow-hidden and min-w-0 to prevent horizontal scrollbar -->
<div class="flex justify-center md:justify-start overflow-hidden min-w-0">
  <AnimatePresence let:item list={[{ key: currentWordIndex }]}>
    <!-- Added overflow-hidden and will-change-transform for better performance -->
    <div class="flex overflow-hidden will-change-transform">
      {#if showWord}
        {#each wordsSplit as char, i}
          <Motion
            initial="hidden"
            animate={isAnimatingOut ? "exit" : "visible"}
            variants={framerProps}
            transition={{
              duration: duration,
              delay: i * delayMultiple,
            }}
            let:motion
          >
            <!-- Added transform-gpu for hardware acceleration -->
            <span use:motion class={cn("drop-shadow-sm transform-gpu", className)}>
              {#if char === " "}
                <span>&nbsp;</span>
              {:else}
                {char}
              {/if}
            </span>
          </Motion>
        {/each}
      {:else}
        <!-- Invisible placeholder to maintain space -->
        {#each wordsSplit as char, i}
          <span class={cn("drop-shadow-sm", className)} style="opacity: 0;">
            {#if char === " "}
              <span>&nbsp;</span>
            {:else}
              {char}
            {/if}
          </span>
        {/each}
      {/if}
    </div>
  </AnimatePresence>
</div>