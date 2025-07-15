<script>
	import ButtonGradient from '$lib/components/GradientAnimation/GradientButton.svelte';
	import { onMount } from "svelte";
	import { tweened } from "svelte/motion";
	import { cubicOut } from "svelte/easing";

	export let y;
	
	let tabs = [
		{
			name: 'Projects',
			link: '#projects'
		},
		{
			name: 'About Me',
			link: '#about'
		}
	];

	// Tweened opacity for smooth button transitions
	const buttonOpacity = tweened(0, {
		duration: 400,
		easing: cubicOut
	});

	let threshold = 0.8; // When to start fading (0.8 = 80% of viewport height)

	onMount(() => {
		const handleScroll = () => {
			const scrollY = window.scrollY;
			const viewportHeight = window.innerHeight;
			const fadeThreshold = viewportHeight * threshold;
			
			// Fade in when scrolled beyond threshold, fade out when within default view
			if (scrollY > fadeThreshold) {
				buttonOpacity.set(1);
			} else {
				buttonOpacity.set(0);
			}
		};

		// Initial check
		handleScroll();
		
		// Add scroll listener
		window.addEventListener('scroll', handleScroll, { passive: true });
		
		// Cleanup
		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
	});
</script>

<header
	class={'sticky z-[10] top-0 duration-300 px-6 flex items-center justify-between border border-solid ' +
		(y > 0 ? 'py-4 bg-slate-950 border-violet-950' : 'py-6 bg-transparent border-transparent')}>
	<h1 class="font-medium">
		<b class="font-bold montserrat">Reniel</b> Peruda
	</h1>
	<div class="sm:flex ml-auto pr-4 items-center gap-4 hidden">
		{#each tabs as tab, index}
			<a href={tab.link} class="duration-300 hover:text-violet-400">
				<p class="montserrat">{tab.name}</p>
			</a>
		{/each}
	</div>
	<div class="flex" style="opacity: {$buttonOpacity}; pointer-events: {$buttonOpacity > 0.1 ? 'auto' : 'none'};">
		<ButtonGradient className="blueShadow relative overflow-hidden px-5 py-2 group rounded-full bg-white text-slate-950 transition-all duration-300">
			Get in touch &rarr;
		</ButtonGradient>
	</div>
</header>