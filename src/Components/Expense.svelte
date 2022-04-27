<script>
	import { getContext } from 'svelte';
	import { slide, fly } from 'svelte/transition';

	export let id;
	export let name = '';
	export let amount = 0;

	let displayAmount = false;

	function toggleAmount() {
		displayAmount = !displayAmount;
	}

	const { removeExpense, handleSetEdit } = getContext('state');
</script>

<article class="single-expense">
	<div class="expense-info">
		<h2>
			{name}
			<button on:click={toggleAmount} class="amount-btn">
				{#if displayAmount}
					-
				{:else}
					+
				{/if}
			</button>
		</h2>
		{#if displayAmount}
			<h4 transition:slide>Amount: ${amount}</h4>
		{/if}
	</div>
	<div class="expense-buttons">
		<button class="expense-btn edit-btn" on:click={() => handleSetEdit(id)}
			>Edit</button
		>
		<button
			class="expense-btn delete-btn"
			on:click={() => removeExpense(id)}>Delete</button
		>
	</div>
</article>

<style>
	.single-expense {
		display: flex;
		justify-content: space-between;
		text-transform: capitalize;
		align-items: center;
		margin-bottom: 2rem;
		padding: 1.3rem 1rem;
		border-radius: var(--mainBorderRadius);
		background: var(--mainWhite);
		box-shadow: var(--lightShadow);
	}

	.single-expense h2 {
		margin-bottom: 0;
		font-weight: 300;
	}

	.single-expense h4 {
		margin-bottom: 0;
		margin-top: 1rem;
		font-weight: 300;
		color: var(--primaryColor);
	}

	.expense-btn {
		font-size: 1rem;
		background: transparent;
		border: none;
		margin: 0 0.4rem;
		transition: var(--mainTransition);
		cursor: pointer;
	}

	.expense-btn:hover {
		transform: scale(1.2);
	}

	.amount-btn {
		font-size: 1.3rem;
		background: transparent;
		border: none;
		cursor: pointer;
		color: var(--primaryColor);
	}

	.delete-btn {
		color: red;
	}

	.edit-btn {
		color: green;
	}
</style>
