<script>
	import Title from './Title.svelte';
	import Expense from './Expense.svelte';
	export let expenses = [];
</script>

<section>
	<Title title="Expenses:" />
	{#each expenses as expense}
		<Expense {...expense} />
	{:else}
		<p>No expenses yet.</p>
	{/each}
</section>

<style>
	section > p {
		text-transform: capitalize;
	}
</style>
