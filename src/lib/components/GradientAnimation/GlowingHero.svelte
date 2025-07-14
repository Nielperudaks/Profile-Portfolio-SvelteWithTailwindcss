<script lang="ts">
  import { onMount } from 'svelte';
  
  let { 
    src = "/src/lib/assets/profile.png",
    alt = "Profile",
    size = "w-80 h-80",
    glowColor = "from-blue-400 via-purple-500 to-pink-500",
    animationSpeed = "3s"
  } = $props();

  let containerRef: HTMLDivElement;
  let mounted = $state(false);

  onMount(() => {
    mounted = true;
  });
</script>

<div 
  bind:this={containerRef}
  class="relative inline-block {size}"
  style="--animation-speed: {animationSpeed};"
>
  <!-- Rotating glow border -->
  <div class="absolute inset-3 rounded-full bg-gradient-to-r {glowColor} opacity-75 blur-md animate-spin-slow"></div>
  
  <!-- Secondary rotating glow (opposite direction) -->
  <div class="absolute inset-3 rounded-full bg-gradient-to-l {glowColor} opacity-50 blur-lg animate-spin-reverse"></div>
  
  <!-- Pulsing outer glow -->
  <div class="absolute inset-2 rounded-full bg-gradient-radial from-transparent via-blue-400/20 to-purple-500/30 animate-pulse-glow"></div>
  
  <!-- Moving light particles -->
  <div class="absolute inset-0  rounded-full overflow-hidden">
    {#if mounted}
      {#each Array(6) as _, i}
        <div 
          class="absolute w-2 h-2 bg-slate rounded-full opacity-60 animate-orbit"
          style="
            --delay: {i * 0.5}s;
            --radius: {120 + i * 10}px;
            animation-delay: var(--delay);
          "
        ></div>
      {/each}
    {/if}
  </div>
  
  <!-- Main image container -->
  <div class="relative z-9 w-full h-full rounded-full overflow-hidden ">
    <img 
      {src} 
      {alt}
      class="w-full h-full object-cover rounded-full"
    />
    
    <!-- Subtle inner glow -->
    <div class="absolute inset-0 rounded-full bg-gradient-to-tr from-transparent via-white/10 to-transparent"></div>
  </div>
  
  <!-- Floating sparkles -->
  {#if mounted}
    {#each Array(8) as _, i}
      <div 
        class="absolute w-1 h-1 bg-white rounded-full opacity-80 animate-float"
        style="
          top: {Math.random() * 100}%;
          left: {Math.random() * 100}%;
          animation-delay: {i * 0.3}s;
          animation-duration: {2 + Math.random() * 2}s;
        "
      ></div>
    {/each}
  {/if}
</div>

<style>
  @keyframes spin-slow {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  
  @keyframes spin-reverse {
    from { transform: rotate(360deg); }
    to { transform: rotate(0deg); }
  }
  
  @keyframes pulse-glow {
    0%, 100% { 
      opacity: 0.3;
      transform: scale(1);
    }
    50% { 
      opacity: 0.6;
      transform: scale(1.05);
    }
  }
  
  @keyframes orbit {
    from {
      transform: rotate(0deg) translateX(var(--radius)) rotate(0deg);
    }
    to {
      transform: rotate(360deg) translateX(var(--radius)) rotate(-360deg);
    }
  }
  
  @keyframes float {
    0%, 100% {
      transform: translateY(0px) scale(1);
      opacity: 0.8;
    }
    50% {
      transform: translateY(-20px) scale(1.2);
      opacity: 0.4;
    }
  }
  
  .animate-spin-slow {
    animation: spin-slow var(--animation-speed) linear infinite;
  }
  
  .animate-spin-reverse {
    animation: spin-reverse calc(var(--animation-speed) * 1.5) linear infinite;
  }
  
  .animate-pulse-glow {
    animation: pulse-glow 2s ease-in-out infinite;
  }
  
  .animate-orbit {
    animation: orbit 4s linear infinite;
  }
  
  .animate-float {
    animation: float 3s ease-in-out infinite;
  }
  
  .bg-gradient-radial {
    background: radial-gradient(circle, var(--tw-gradient-stops));
  }
</style>
