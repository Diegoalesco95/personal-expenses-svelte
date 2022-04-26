<nav class="nav">
	<div class="nav-center">
		<h1 class="nav-title">Budget Calculator</h1>
		<button type="button" class="nav-btn">+ Add Item</button>
	</div>
</nav>

<style>
	.nav {
		background: var(--primaryColor);
		height: 5rem;
		display: flex;
		align-items: center;
		box-shadow: var(--lightShadow);
	}

	.nav-center {
		width: 85%;
		max-width: 35rem;
		margin: 0 auto;
		display: flex;
		justify-content: space-between;
	}

	.nav-title {
		text-transform: capitalize;
		color: var(--mainWhite);
		margin-bottom: 0;
		letter-spacing: 2px;
	}

	.nav-btn {
		background: transparent;
		border: 1px solid var(--mainWhite);
		border-radius: 4px;
		color: var(--mainWhite);
		cursor: pointer;
		font-size: 1.3rem;
		padding: 0.5rem;
		text-transform: capitalize;
		transition: var(--mainTransition);
	}

	.nav-btn:hover {
		color: var(--darkGrey);
	}
</style>
