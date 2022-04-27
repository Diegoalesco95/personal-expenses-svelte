<script>
	import { getContext } from 'svelte';

	import Title from './Title.svelte';

	export let id = null;
	export let name = '';
	export let amount = 0;
	export let handleShowForm;

	const { addExpense, updateExpense } = getContext('state');

	$: isEmpty = !name || !amount;
	$: isEditing = !!id;

	function handleCloseForm() {
		handleShowForm(false, true);
	}

	function handleSubmit(e) {
		e.preventDefault();
		if (isEditing) {
			updateExpense(id, { id, name, amount });
		} else {
			addExpense({ name, amount });
		}
		handleCloseForm();
	}
</script>

<section class="form">
	<Title title={isEditing ? 'Edit Expense:' : 'Add Expense:'} />
	<form class="expense-form" on:submit={handleSubmit}>
		<div class="form-control">
			<label for="name">Name</label>
			<input type="text" id="name" bind:value={name} />
		</div>
		<div class="form-control">
			<label for="amount">Amount</label>
			<input type="number" id="amount" bind:value={amount} />
		</div>
		{#if isEmpty}
			<p class="form-empty">Please, fill out al form fields</p>
		{/if}
		<button
			disabled={isEmpty}
			type="submit"
			class="btn btn-block"
			class:disabled={isEmpty}
		>
			{isEditing ? 'Update Expense' : 'Add Expense'}
		</button>
	</form>
	<button class="close-btn" on:click={() => handleCloseForm()}> Close</button>
</section>

<style>
	.expense-form {
		background: var(--mainWhite);
		padding: 1.25rem 1rem;
		text-transform: capitalize;
		border-radius: var(--mainBorderRadius);
	}

	.form-control label {
		display: block;
	}

	.form-control input {
		width: 100%;
		border: none;
		border-bottom: 2px solid var(--darkGrey);
		margin-bottom: 1.25rem;
		padding: 0.5rem;
		font-size: 1.2rem;
	}

	.form-empty {
		text-align: center;
		color: red;
	}

	.form {
		position: relative;
		margin-bottom: 5rem;
	}
</style>
