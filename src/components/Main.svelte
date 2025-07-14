<script>
	import Step from './Step.svelte';
	import GradualSpacing from '$lib/components/TextAnimation/TextSpace.svelte';
	import Gradientbutton from '$lib/components/GradientAnimation/GradientButton.svelte';
	import GradualSpacingCycle from '$lib/components/TextAnimation/TextSpaceCycle.svelte';
	import GlowingHero from '$lib/components/GradientAnimation/GlowingHero.svelte';

	import HeroParallax from '$lib/components/CardAnimations/InfiniteMovingCards.svelte';
	import Marquee from '$lib/components/CardAnimations/Marquee.svelte';

	const products = [
		{
			title: 'git',
			link: '',
			thumbnail: 'Logo/9.png'
		},
		{
			title: 'Python',
			link: '',
			thumbnail: 'Logo/5.png'
		},
		{
			title: 'JavaScript',
			link: '',
			thumbnail: 'Logo/10.png'
		},

		{
			title: 'Svelte',
			link: '',
			thumbnail: 'Logo/2.png'
		},
		{
			title: 'React',
			link: '',
			thumbnail: 'Logo/1.png'
		},
		{
			title: 'git',
			link: '',
			thumbnail: 'Logo/9.png'
		},

		{
			title: 'C#',
			link: '',
			thumbnail: 'Logo/3.png'
		},
		{
			title: 'PHP',
			link: '',
			thumbnail: 'Logo/6.png'
		},
		{
			title: 'CSS',
			link: '',
			thumbnail: 'Logo/7.png'
		},
		{
			title: 'Html',
			link: '',
			thumbnail: 'Logo/8.png'
		},
		{
			title: 'git',
			link: '',
			thumbnail: 'Logo/9.png'
		},

		{
			title: 'Sql',
			link: '',
			thumbnail: 'Logo/11.png'
		},
		{
			title: 'Figma',
			link: '',
			thumbnail: 'Logo/12.png'
		},
		{
			title: 'Laravel',
			link: '',
			thumbnail: 'Logo/13.png'
		},
		{
			title: 'Java',
			link: '',
			thumbnail: 'Logo/4.png'
		}
	];

	let steps = [
		{
			name: 'PHP',
			icon: 'https://img.icons8.com/?size=100&id=9BGchbZAXAyR&format=png&color=FFFFFF',
			img: 'images/php-dental.png',
			link: 'https://github.com/Nielperudaks/Franco-Pascual-Dental-Clinic-Web-Based-Online-Appointment-System'
		},
		{
			name: 'Svelte',
			icon: 'https://img.icons8.com/?size=75&id=7ST6T6xV3OPb&format=png&color=FFFFFF',
			img: 'images/svelte-profile.png',
			link: 'https://github.com/Nielperudaks/Profile-Portfolio-SvelteWithTailwindcss'
		}
	];
	let benefits = [
		{
			name: 'self taught',
			description:
				'I’m a self-taught developer who learned by building, breaking, and improving real projects. My curiosity and dedication drive me to keep growing and adapting in this ever-evolving tech space.'
		},
		{
			name: 'a product design and UX Fanatic',
			description:
				'I’m passionate about creating clean, user-focused designs. I care deeply about how things feel and function, always aiming to craft intuitive, delightful experiences that solve real problems.'
		},
		{
			name: 'an excellent communicator',
			description:
				'Whether it’s collaborating with teams or explaining ideas clearly to non-tech folks, I value open and effective communication. I believe great products are built through clear dialogue and shared understanding.'
		}
	];
</script>

<main class="flex flex-col flex-1 p-4">
	<section id="introPage" class=" grid grid-cols-1 lg:grid-cols-2 gap-10 py-8 sm:py-14 lg:my-12">
		<div class="flex flex-col lg:justify-center text-center lg:text-left gap-6 md:gap-8 lg:gap-10">
			<h2 class="font-semibold text-2xl sm:4xl md:5xl">
				<GradualSpacing class="montserrat -mb-12" words="Hi! I'm" /> <br />
				<GradualSpacing
					class="montserrat -mb-6 text-violet-400 text-8xl sm:text-9xl font-extrabold"
					words="Reniel"
				/>
				<!-- <span class="montserrat text-5xl sm:text-9xl font-light">Peruda</span> -->
				<GradualSpacing class="montserrat  text-8xl sm:text-9xl font-light" words="Peruda" />
				<!-- <br /><GradualSpacing class="montserrat text-3xl font-extralight" words="Full Stack Developer"/> -->
				<GradualSpacingCycle
					class="montserrat text-2xl sm:text-3xl  font-extralight"
					words={['Full Stack Developer', 'UI/UX Designer', 'Creative Coder', 'Problem Solver']}
					cycleDuration={3000}
				/>
			</h2>

			<div class="flex">
				<Gradientbutton
					className="blueShadow mx-auto lg:mr-auto lg:ml-0 text-base sm:text-lg md:text-xl montserrat relative overflow-hidden px-6 py-3 group rounded-full bg-white text-slate-950"
					>Get in touch &rarr;</Gradientbutton
				>
			</div>
		</div>
		<div class="relative grid place-items-center">
			<GlowingHero
				src={'images/profile.png'}
				alt="Profile Picture"
				size="w-96 h-100 lg:w-[28rem] lg:h-[33rem]"
				glowColor="from-pink-550 via-purple-450 to-violet-500"
				animationSpeed="15s"
			/>
		</div>
	</section>
	<section id="skills" class="py-20 lg:py-32 flex flex-col gap-24">
		<div class="flex flex-col gap-2 sm:text-left text-center">
			<h3 class="montserrat font-semibold text-4xl sm:text-5xl md:text-6xl">
				My Core <span class="montserrat text-violet-400">Skills </span>
			</h3>
			<h6 class="text-lg sm:text-xl md:text-2xl montserrat font-light">
				Years of knowledge gathering.
			</h6>
		</div>
		<Marquee />
	</section>
	<section id="projects" class="py-20 lg:py-32 flex flex-col gap-24">
		<div class="flex flex-col gap-2 text-center">
			<h6 class="text-lg sm:text-xl md:text-2xl">A few of my creative endeavors.</h6>
			<h3 class="font-semibold text-3xl sm:text-4xl md:text-5xl">
				Curious to <span class="montserrat text-violet-400">see </span> my work?
			</h3>
		</div>
		<a
			href="https://github.com/Nielperudaks"
			target="_blank"
			class="mx-auto px-4 py-2 rounded-md border border-solid border-white
            flex items-center gap-2 -mb-4 sm:-mb-0 -mt-10 hover:border-violet-700 duration-300"
		>
			<i class="fa-regular fa-circle-play"></i>
			<p>Check my Github</p>
		</a>
		<div class="grid grid-cols-1 lg:grid-cols-2 gap-12 lg:gap-10">
			<Step step={steps[0]}>
				<p class="montserrat font-light">
					The <strong class="text-violet-400">
						Franco-Pascual Dental Clinic Online Appointment System</strong
					>
					is designed to enhance patient engagement and clinic efficiency through advanced features
					and seamless functionality. At its core is an interactive 3D teeth model developed with
					<strong class="text-violet-400">Three.js</strong>
				</p>
			</Step>
			<Step step={steps[1]}>
				<p class="montserrat font-light">
					<strong class="text-violet-400">A modern, fast, and responsive portfolio built with Svelte and Tailwind CSS.</strong> Showcasing my
					projects, skills, and experience through a minimalist design, smooth animations, and
					blazing-fast performance — all made possible with the power of Svelte's reactivity and
					Tailwind's utility-first styling.
				</p>
			</Step>
		</div>
	</section>
	<section
		id="about"
		class="py-20 pt-10 lg:pt-16 lg:py-32 flex flex-col gap-16 sm:gap-20 md:gap-24 relative"
	>
		<div
			class="flex flex-col gap-2 text-center relative before:absolute before:top-0 before:left-0 before:w-2/3
        before:h-1.5 before:bg-violet-700 after:absolute after:bottom-0 after:right-0 after:w-2/3
        after:h-1.5 after:bg-violet-700 py-4"
		>
			<h6 class="text-lg sm:text-xl md:text-2xl">Want to know more?</h6>
			<h3 class="font-semibold text-3xl sm:text-4xl md:text-5xl">
				A bit <span class="montserrat text-violet-400">about</span> me
			</h3>
		</div>
		<p class="mx-auto montserrat font-semibold text-lg sm:text-xl md:text-2xl">I am...</p>
		<div class="flex flex-col gap-20 w-full mx-auto max-w-[800px]">
			{#each benefits as benefit, index}
				<div class="flex gap-6 sm:gap-8">
					<p class="montserrat text-4xl sm:text-5xl md:text-6xl font-semibold text-slate-500">
						0{index + 1}
					</p>
					<div class="flex flex-col gap-6 sm:gap-8">
						<h3 class="text-2xl sm:text-3xl md:text-5xl">
							{benefit.name}
						</h3>
						<p class="montserrat font-light">{benefit.description}</p>
					</div>
				</div>
			{/each}
		</div>
		<h5 class="text-2xl sm:text-3xl text-semibold text-center montserrat">
			The <span class="text-violet-400 montserrat">Complete</span> Package
		</h5>
		<div class="flex flex-col overflow-x-scroll gap-10 max-w-[800px] mx-auto w-full">
			<table class="bg-white text-slate-700 rounded text-center">
				<thead class="border-b border-solid border-slate-200">
					<tr class="">
						<th></th>
						<th class="whitespace-nowrap p-2 px-4">Candidate 1</th>
						<th class="whitespace-nowrap p-2 px-4">Candidate 2</th>
						<th class="whitespace-nowrap p-2 px-4">Candidate 3</th>
						<th class="whitespace-nowrap bg-violet-700 text-white p-4 px-8">Me</th>
					</tr>
				</thead>
				<tbody>
					<tr class="border-b border-solid border-slate-200">
						<td class="border-r border-solid border-white pl-4 pr-8 py-4 font-semibold text-sm"
							>Dedication</td
						>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-check text-green-500"></i></td>
					</tr>
					<tr class="border-b border-solid border-slate-200">
						<td class="border-r border-solid border-white pl-4 pr-8 py-4 font-semibold text-sm"
							>Perseverance</td
						>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-check text-green-500"></i></td>
					</tr>
					<tr class="border-b border-solid border-slate-200">
						<td class="border-r border-solid border-white pl-4 pr-8 py-4 font-semibold text-sm"
							>Passion</td
						>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-check text-green-500"></i></td>
					</tr>
					<tr class="border-b border-solid border-slate-200">
						<td class="border-r border-solid border-white pl-4 pr-8 py-4 font-semibold text-sm"
							>Mastery</td
						>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-xmark text-slate-500"></i></td>
						<td><i class="fa-solid fa-check text-green-500"></i></td>
					</tr>
				</tbody>
			</table>
		</div>
		<div class="mx-auto -mt-12 italic sm:hidden opacity-50">
			<p>Scroll to see more &rarr;</p>
		</div>
		<p class="mx-auto">So why not Invest?</p>
	</section>
</main>
