<script lang="ts">
	import type { CounterType } from '../types/CounterType';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let currentValue: CounterType;

	const handleInputChange = (event: any) => {
		currentValue.title = event.target.value;
		dispatch('changedCurrentValue', currentValue);
	};

	const onClickChange = (val: number) => {
		if (currentValue.count == 0 && val == -1) {
			return;
		}
		currentValue.count += val;
		dispatch('changedCurrentValue', currentValue);
	};

	const onClickResetValue = () => {
		currentValue.count = 0;
		dispatch('changedCurrentValue', currentValue);
	};

	const onClickRemoveCounter = () => {
		dispatch('removeCurrentCounter', currentValue);
	};
</script>

<div
	class="max-w-sm rounded border-solide bg-gray-100 shadow-lg m-auto flex relative items-center mb-2 py-[4px]"
>
	<input
		on:input={handleInputChange}
		class="text-gray-600 mx-4 px-1 w-32 outline-none"
		bind:value={currentValue.title}
	/>
	<span class="text-lg font-bold px-4">
		{currentValue.count}
	</span>
	<div class="ml-auto flex justify-end">
		<button
			on:click={() => {
				onClickChange(1);
			}}
			class="text-white cursor-pointer hover:opacity-85 transition-all duration-300 text-[18px] px-[12px] py-[4px] bg-red-500 rounded-l"
			>+</button
		>
		<button
			on:click={() => {
				onClickChange(-1);
			}}
			class="text-white cursor-pointer hover:opacity-85 transition-all duration-300 text-[18px] px-[12px] py-[4px] bg-blue-500"
			>-</button
		>
		<button
			on:click={() => {
				onClickResetValue();
			}}
			class="text-white cursor-pointer hover:opacity-85 transition-all duration-300 text-[18px] px-[12px] py-[4px] bg-yellow-500 rounded-r"
			>0</button
		>
		<button
			on:click={() => onClickRemoveCounter()}
			class="text-gray-500 hover:opacity-85 transition-all duration-300 cursor-pointer px-4"
			>x</button
		>
	</div>
</div>
