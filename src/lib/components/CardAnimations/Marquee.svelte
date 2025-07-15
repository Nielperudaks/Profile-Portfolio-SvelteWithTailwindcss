<!-- MarqueeLogos.svelte -->
<script>
  const products = [
    { title: 'git',       thumbnail: 'Logo/9.png' },
    { title: 'Python',    thumbnail: 'Logo/5.png' },
    { title: 'JavaScript',thumbnail: 'Logo/10.png'},
    { title: 'Svelte',    thumbnail: 'Logo/2.png' },
    { title: 'React',     thumbnail: 'Logo/1.png' },
    { title: 'C#',        thumbnail: 'Logo/3.png' },
    { title: 'PHP',       thumbnail: 'Logo/6.png' },
    { title: 'CSS',       thumbnail: 'Logo/7.png' },
    { title: 'Html',      thumbnail: 'Logo/8.png' },
    { title: 'Sql',       thumbnail: 'Logo/11.png'},
    { title: 'Figma',     thumbnail: 'Logo/12.png'},
    { title: 'Laravel',   thumbnail: 'Logo/13.png'},
    { title: 'Java',      thumbnail: 'Logo/4.png' },
	{ title: 'git',       thumbnail: 'Logo/9.png' },
    { title: 'Python',    thumbnail: 'Logo/5.png' },
    { title: 'JavaScript',thumbnail: 'Logo/10.png'},
    { title: 'Svelte',    thumbnail: 'Logo/2.png' },
    { title: 'React',     thumbnail: 'Logo/1.png' },
    { title: 'C#',        thumbnail: 'Logo/3.png' },
    { title: 'PHP',       thumbnail: 'Logo/6.png' },
    { title: 'CSS',       thumbnail: 'Logo/7.png' },
    { title: 'Html',      thumbnail: 'Logo/8.png' },
    { title: 'Sql',       thumbnail: 'Logo/11.png'},
    { title: 'Figma',     thumbnail: 'Logo/12.png'},
    { title: 'Laravel',   thumbnail: 'Logo/13.png'},
    { title: 'Java',      thumbnail: 'Logo/4.png' }
  ];

  const items = [...products, ...products];
  
  let activeTappedIndex = $state(null);
  let tapTimer = null;

  function handleTap(index) {
    // Clear any existing timer
    if (tapTimer) {
      clearTimeout(tapTimer);
    }
    
    // Show tooltip for this item
    activeTappedIndex = index;
    
    // Auto-hide tooltip after 2 seconds
    tapTimer = setTimeout(() => {
      activeTappedIndex = null;
    }, 2000);
  }

  function handleClickOutside(event) {
    // Hide tooltip when clicking outside
    if (!event.target.closest('.logo-item')) {
      activeTappedIndex = null;
      if (tapTimer) {
        clearTimeout(tapTimer);
      }
    }
  }
</script>

<svelte:window on:click={handleClickOutside} />

<!-- wrapper keeps the padding / boundaries -->
<div class="relative w-full isolate overflow-hidden pt-10 ">
  <!-- left fade -->
  <div class="absolute  top-0 left-0 z-10 h-full w-24 bg-gradient-to-r from-slate-950 via-slate-950/60 to-transparent pointer-events-none" />
  <!-- right fade -->
  <div class="absolute top-0 right-0 z-10 h-full w-24 bg-gradient-to-l from-slate-950 via-slate-950/60 to-transparent pointer-events-none" />

  <!-- scrolling row (relative so it respects parent padding) -->
  <div class="relative flex h-30 sm:h-40 items-center">
    <div class="flex animate-marquee items-center space-x-20">
      {#each items as { title, thumbnail }, index}
        <div 
          class="relative group flex-shrink-0 logo-item cursor-pointer"
          on:click={() => handleTap(index)}
          on:keydown={(e) => e.key === 'Enter' && handleTap(index)}
          tabindex="0"
          role="button"
          aria-label="Show {title} tooltip"
        >
          <img
            src={thumbnail}
            alt={title}
            class="sm:h-40 h-30 w-auto object-contain transition-transform duration-300 group-hover:scale-110"
          />
          <div 
            class="absolute -top-9 left-1/2 -translate-x-1/2
                   rounded-md bg-slate-700 px-2 py-1 text-sm text-white
                   transition-opacity duration-200 pointer-events-none z-20
                   {activeTappedIndex === index ? 'opacity-100' : 'opacity-0 group-hover:opacity-100'}"
          >
            {title}
          </div>
        </div>
      {/each}
    </div>
  </div>
</div>

<style>
  @keyframes marquee {
    0%   { transform: translateX(0%); }
    100% { transform: translateX(-76.5%); }
  }

  :global(.animate-marquee) {
    animation: marquee 30s linear infinite;
  }

  /* Hide focus outline on mobile but keep for keyboard navigation */
  .logo-item:focus {
    outline: 2px solid transparent;
  }

  .logo-item:focus-visible {
    outline: 2px solid #8b5cf6;
    outline-offset: 2px;
  }
</style>