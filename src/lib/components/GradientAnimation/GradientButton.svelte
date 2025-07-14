<script>
	import { onMount } from 'svelte';
    import { cn } from '$lib/utils/cn';

    let { className = ''}= $props();
    
	
	let buttonRef = $state(null);
	let orbX = $state(50);
	let orbY = $state(50);
	let isHovered = $state(false);
	let isShining = $state(false);
	
	// Floating orb animation on hover
	function handleMouseEnter() {
		isHovered = true;
		animateOrb();
	}
	
	function handleMouseLeave() {
		isHovered = false;
	}
	
	function animateOrb() {
		if (!isHovered) return;
		
		// Random movement within the button bounds
		orbX = Math.random() * 80 + 10; // 10% to 90%
		orbY = Math.random() * 60 + 20; // 20% to 80%
		
		// Continue animation while hovered
		setTimeout(() => {
			if (isHovered) animateOrb();
		}, 800);
	}
	
	// Shining text effect every 3 seconds
	onMount(() => {
		const shineInterval = setInterval(() => {
			isShining = true;
			setTimeout(() => {
				isShining = false;
			}, 600);
		}, 3000);
		
		return () => clearInterval(shineInterval);
	});
    
</script>


	<a 
		href="#"
		target="_blank"
		class={cn(className," transition-all duration-300 hover:scale-105")}
		
		onmouseenter={handleMouseEnter}
		onmouseleave={handleMouseLeave}
	>
		<!-- Floating gradient orb -->
		<div 
			class="absolute w-16 h-16 rounded-full opacity-0 group-hover:opacity-30 transition-all duration-700 ease-out pointer-events-none"
			class:animate-pulse={isHovered}
			style="
				left: {orbX}%; 
				top: {orbY}%; 
				transform: translate(-50%, -50%);
				background: radial-gradient(circle, rgb(139 92 246) 0%, rgb(109 40 217) 30%, rgb(71 85 105) 70%, transparent 100%);
				transition: left 0.8s cubic-bezier(0.4, 0, 0.2, 1), top 0.8s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.3s ease;
			"
		></div>
		
		<!-- Shining text -->
		<h4 
			class="relative z-10 font-medium text-lg transition-all duration-300"
			class:shine={isShining}
		>
        <slot/>
			 
		</h4>
		
		<!-- Additional subtle gradient overlay -->
		<div class="absolute inset-0 bg-gradient-to-r from-violet-500/5 via-slate-500/5 to-violet-500/5 opacity-0 group-hover:opacity-100 transition-opacity duration-500 rounded-full"></div>
	</a>


<style>
	.blueShadow {
		box-shadow: 0 4px 14px 0 rgba(139, 92, 246, 0.15);
		transition: box-shadow 0.3s ease;
	}
	
	.blueShadow:hover {
		box-shadow: 0 6px 20px 0 rgba(139, 92, 246, 0.25);
	}
	
	.shine {
		background: linear-gradient(
			90deg,
			rgb(71 85 105) 0%,
			rgb(139 92 246) 25%,
			rgb(255 255 255) 50%,
			rgb(139 92 246) 75%,
			rgb(71 85 105) 100%
		);
		background-size: 200% 100%;
		background-clip: text;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		animation: shine-sweep 0.6s ease-in-out;
	}
	
	@keyframes shine-sweep {
		0% {
			background-position: -200% 0;
		}
		100% {
			background-position: 200% 0;
		}
	}
	
	/* Additional orb glow effect */
	.group:hover .absolute:first-of-type {
		filter: blur(8px);
	}
</style>
