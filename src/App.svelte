<script>
	import Nabvar from './Components/Nabvar.svelte';
	import Title from './Components/Title.svelte';
	import Expenses from './Components/Expenses.svelte';
	import expenses from './helpers/expenses';
</script>

<Nabvar />
<main class="content">
	<Title title="Add Expense:" />
	<Expenses {expenses} />
</main>

<style>
	.content {
		padding: 3rem 0;
		width: 85vw;
		max-width: 35rem;
		margin: 0 auto;
	}
</style>
