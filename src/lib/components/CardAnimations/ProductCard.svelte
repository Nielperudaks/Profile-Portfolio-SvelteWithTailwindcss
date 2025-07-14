<script lang="ts">
	import { Motion, MotionValue } from 'svelte-motion';

	export let product: {
		title: string;
		link: string;
		thumbnail: string;
	};
	export let translate: MotionValue<number>;

	let isHovered = false;
	let mouseX = 0;
	let mouseY = 0;

	function handleMouseMove(event: MouseEvent) {
		const rect = event.currentTarget.getBoundingClientRect();
		mouseX = event.clientX - rect.left;
		mouseY = event.clientY - rect.top;
	}
</script>

<style>
	.tooltip {
		position: absolute;
		background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
		color: white;
		padding: 12px 16px;
		border-radius: 12px;
		font-size: 14px;
		font-weight: 500;
		white-space: nowrap;
		opacity: 0;
		visibility: hidden;
		transition: opacity 0.2s ease, visibility 0.2s ease;
		box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
		backdrop-filter: blur(10px);
		z-index: 1000;
		pointer-events: none;
		transform: translate(-50%, -100%);
		margin-top: -10px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.tooltip::before {
		content: '';
		position: absolute;
		top: 100%;
		left: 50%;
		transform: translateX(-50%);
		border: 6px solid transparent;
		border-top-color: #667eea;
	}

	.tooltip.show {
		opacity: 1;
		visibility: visible;
	}
</style>

<Motion
	let:motion
	style={{
		x: translate
	}}
	whileHover={{
		y: -20
	}}
>
	<div
		use:motion
		class="group/product relative h-[10rem] w-[10rem] sm:h-[20rem] sm:w-[20rem] flex-shrink-0"
		on:mouseenter={() => isHovered = true}
		on:mouseleave={() => isHovered = false}
		on:mousemove={handleMouseMove}
	>
		<a href={product.link} class="block group-hover/product:shadow-2xl">
			<img
				src={product.thumbnail}
				height="600"
				width="600"
				class="absolute inset-0 h-full w-full object-cover object-left-top"
				alt={product.title}
			/>
		</a>
		<div
			class="pointer-events-none absolute inset-0 h-full w-full bg-black/20 opacity-0 group-hover/product:opacity-80 transition-opacity duration-300"
		></div>
		<div 
			class="tooltip" 
			class:show={isHovered}
			style="left: {mouseX}px; top: {mouseY}px;"
		>
			{product.title}
		</div>
	</div>
</Motion>