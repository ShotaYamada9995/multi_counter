<script lang="ts">
	export let removeCounter: (id: number) => void,
		counter: { id: number; title: string; count: number };
	import { createEventDispatcher } from "svelte";

	const dispatch = createEventDispatcher();

	function addCount() {
		counter.count += 1;
		dispatch("countChange", counter.count);
	}
	function removeCount() {
		if (counter.count > 0) {
			counter.count -= 1;
			dispatch("countChange", counter.count);
		}
	}
	function resetCount() {
		counter.count = 0;
		dispatch("countChange", counter.count);
	}
	function handleRemove() {
		removeCounter(counter.id);
	}
	function handleTitleChange(event: Event) {
		const inputElement = event.target as HTMLInputElement;
		if (inputElement instanceof HTMLInputElement) {
			counter.title = inputElement.value;
		}
		dispatch("titleChange", counter.title);
	}
</script>

<div
	class="max-w-sm rounded border-solide bg-gray-100 shadow-lg m-auto flex relative items-center mb-2"
>
	<input
		type="text"
		name="title"
		class="text-gray-600 mx-4 px-1 w-32"
		bind:value={counter.title}
		on:input={handleTitleChange}
	/>
	<span class="text-lg font-bold px-4 absolute centerize"
		>{counter.count}</span
	>
	<div class="ml-auto">
		<button
			on:click={addCount}
			class="text-white bg-red-500 rounded-l text-lg py-1 px-3 my-1"
			>+</button
		>
		<button
			on:click={removeCount}
			class="text-white bg-blue-500 text-lg py-1 px-3 my-1">-</button
		>
		<button
			on:click={resetCount}
			class="text-white bg-yellow-500 rounded-r text-lg py-1 px-3 my-1"
			>0</button
		>
		<button
			on:click={handleRemove}
			class="text-gray-500 cursor-pointer px-4">x</button
		>
	</div>
</div>

<style>
	.centerize {
		left: 50%;
		transform: translateX(-50%);
	}
</style>
