<script>
	export let step;
	import CardBody from '$lib/components/ThreeDcardEffect/CardBody.svelte';
	import CardContainer from '$lib/components/ThreeDcardEffect/CardContainer.svelte';
	import CardItem from '$lib/components/ThreeDcardEffect/CardItem.svelte';

	let isMouseEntered = false;
</script>

<a
	href={step.href}
	target="_blank"
	class="p-4 sm:p-6 md:p-8 flex flex-col gap-4
	rounded-lg border border-solid border-violet-700 text-center group cursor-pointer hover:border-violet-400 duration-300"
>
	<div
		class="bg-slate-950 grid place-items-center px-4 text-5xl md:6xl -mt-10 sm:-mt-12 md:-mt-14 lg:-mt-16 mx-auto
		duration-300"
	>
		<img src={step.icon} class={step.icon} alt="" />
	</div>
	<h3 class="font-medium text-xl sm:text-2xl md:text-3xl">{step.name}</h3>

	<CardContainer bind:isMouseEntered className="inter-var">
		<CardBody className="">
			<CardItem {isMouseEntered} translateZ="60" className="text-white mt-2 text-sm">
				<slot />
			</CardItem>
			<CardItem {isMouseEntered} translateZ="100" className="w-full mt-4">
				<img
					src={step.img}
					height="1000"
					width="1000"
					class="h-60 w-full rounded-xl object-cover group-hover/card:shadow-xl"
					alt="thumbnail"
				/>
			</CardItem>
			<div class="mt-20 flex items-center justify-between">
				<CardItem
					{isMouseEntered}
					translateZ={20}
					className="ml-auto cursor-pointer hover:text-slate-950 duration-300 relative after:absolute
				after:h-0 after:top-0 after:right-full after:w-full after:h-full after:bg-white after:duration-200
				hover:after:translate-x-full after:z-[-1] overflow-hidden"
				>
					<a href={step.link}>Go to &rarr; </a>
				</CardItem>
			</div>
		</CardBody>
	</CardContainer>
</a>
