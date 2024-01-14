<script lang="ts">
	import { v4 as uuidv4 } from 'uuid';
	import Counter from '../components/Counter.svelte';
	import type { CounterType } from '../types/CounterType';

	let counterData: CounterType[] = [
		{
			id: uuidv4(),
			title: 'new',
			count: 0
		}
	];

	const addNewCounter = () => {
		const newCounter: CounterType = {
			id: uuidv4(),
			title: 'new',
			count: 0
		};
		counterData = [...counterData, newCounter];
	};

	const updateCurrentValue = (event: any) => {
		const idx = counterData.findIndex((item) => item.id == event.detail.id);
		counterData[idx] = event.detail;
	};

	const removeCurrentCounter = (event: any) => {
		counterData = counterData.filter((item) => item.id != event.detail.id);
	};
</script>

<svelte:head>
	<title>Multiple Counter</title>
	<meta name="description" content="Svelte Multiple Counter" />
</svelte:head>

<section>
	<h1 class="text-center text-[64px]">Multiple Counter</h1>
	<div class="max-w-[380px] mx-auto">
		{#each counterData as item (item)}
			<Counter
				currentValue={item}
				on:changedCurrentValue={updateCurrentValue}
				on:removeCurrentCounter={removeCurrentCounter}
			/>
		{/each}
	</div>
	<div class="max-w-sm mx-auto text-center">
		<button
			on:click={addNewCounter}
			class="max-w-sm w-full mx-auto rounded bg-green-400 hover:opacity-75 transition-all duration-300 text-white text-[16px] text-center cursor-pointer"
		>
			new counter
		</button>
		<p>
			title list:
			{counterData.map((item) => item.title)}
		</p>
		<p>
			sum of count:
			{counterData
				.map((item) => Number(item.count))
				.reduce((accumulator, currentValue) => accumulator + currentValue, 0)}
		</p>
	</div>
</section>
