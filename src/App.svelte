<script>
	import { setContext, beforeUpdate, afterUpdate, onMount } from 'svelte';

	import Expenses from './Components/Expenses.svelte';
	import ExpenseForm from './Components/ExpenseForm.svelte';
	import Nabvar from './Components/Nabvar.svelte';
	import Total from './Components/Total.svelte';
	import Modal from './Components/Modal.svelte';

	let expenses = [];

	let showForm = false;
	let currentExpense = {
		id: null,
		name: '',
		amount: 0,
	};

	$: total = expenses.reduce(
		(totalExpense, expense) => totalExpense + expense.amount,
		0
	);

	function addExpense(expense) {
		const newExpense = {
			id: Math.random() * Date.now(),
			...expense,
		};
		expenses = [newExpense, ...expenses];
	}

	function resetValues() {
		currentExpense = { id: null, name: '', amount: 0 };
	}

	function handleShowForm(shouldShowForm, reset = false) {
		showForm = shouldShowForm;
		if (reset) {
			resetValues();
		}
	}

	function modifyCurrentExpense(expense) {
		currentExpense = expense;
	}

	function handleSetEdit(id) {
		const expense = expenses.find((expense) => expense.id === id);
		modifyCurrentExpense(expense);
		handleShowForm(true);
	}

	function removeExpense(id) {
		expenses = expenses.filter((expense) => expense.id !== id);
	}

	function updateExpense(id, expenseUpdated) {
		expenses = expenses.map((expense) =>
			expense.id === id ? { ...expense, ...expenseUpdated } : expense
		);
	}

	function clearAllExpenses() {
		expenses = [];
	}

	// Context

	const state = {
		addExpense,
		handleSetEdit,
		updateExpense,
		removeExpense,
	};

	setContext('state', state);

	// Local Storage

	function setLocalStorage() {
		localStorage.setItem('expenses', JSON.stringify(expenses));
	}

	function getLocalStorage() {
		const expensesLS = localStorage.getItem('expenses');
		if (expensesLS) {
			expenses = JSON.parse(expensesLS);
		}
	}

	// life cycle

	onMount(() => {
		getLocalStorage();
	});

	afterUpdate(() => {
		setLocalStorage();
	});
</script>

<Nabvar {handleShowForm} />
<main class="content">
	{#if showForm}
		<Modal>
			<ExpenseForm {...currentExpense} {handleShowForm} />
		</Modal>
	{/if}
	<Total {total} />
	<Expenses {expenses} />
	{#if expenses.length > 0}
		<button
			class="btn btn-block btn-primary"
			on:click={clearAllExpenses}
			type="button"
		>
			Clear expenses
		</button>
	{/if}
</main>

<style>
	.content {
		padding: 3rem 0;
		width: 85vw;
		max-width: 35rem;
		margin: 0 auto;
	}
</style>
