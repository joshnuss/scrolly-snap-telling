<script>
	import Step1 from "./Step1.svelte"
	import Step2 from "./Step2.svelte"
	import Step3 from "./Step3.svelte"
	
	const steps = [
		{ title: "Scrolly", color: '--red-2', component: Step1 },
		{ title: "Snap", color: '--yellow-3', component: Step2 },
		{ title: "Telling", color: '--lime-2', component: Step3 }
	]
</script>

<main>
	{#each steps as step}
		<section style:background="var({step.color})">
			<span>{step.title}</span>

			<div class="demo">
				<svelte:component this={step.component}/>
			</div>
		</section>
	{/each}
</main>

<style>
	main {
		display: grid;
		flex-direction: column;
		scroll-snap-type: y mandatory;
		max-height: 100vh;
		overflow-y: scroll;
	}

	section {
		scroll-snap-align: start;
		display: grid;
		grid-template-columns: 1fr 1fr;
		align-items: center;
		min-height: 100vh;
		padding: var(--size-12);
		font-size: 6rem;
		color: var(--gray-8);

		& span {
			opacity: 0;
			animation-name: fade-in, scale-up;
			animation-duration: 1ms; /* Firefox requires this to apply the animation */
			animation-timeline: view();
			animation-range: contain;
		}
	}

	.demo {
		display: flex;
		place-self: center;
		align-items: center;
		justify-content: center;
		opacity: 0;
		animation-name: slide-in-left, fade-in;
		animation-timeline: view();
		animation-range: cover;
	}

	.demo :global(svg) {
		width: 20vw;
	}
</style>
