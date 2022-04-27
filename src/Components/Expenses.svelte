<script>
	import { fly } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	import Title from './Title.svelte';
	import Expense from './Expense.svelte';

	export let expenses = [];
</script>

<section>
	<Title title="Expenses:" />
	{#each expenses as expense, index (expense.id)}
		<div
			in:fly={{ x: 200, delay: (index + 1) * 700 }}
			out:fly={{ x: -200 }}
			animate:flip
		>
			<Expense {...expense} on:delete />
		</div>
	{:else}
		<p>No expenses yet.</p>
	{/each}
</section>

<style>
	section > p {
		text-transform: capitalize;
	}
</style>
