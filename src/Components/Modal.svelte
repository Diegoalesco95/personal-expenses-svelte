<script>
	import { blur, fade, fly } from 'svelte/transition';
</script>

<div class="modal-container" in:blur out:fade>
	<div class="modal-content" transition:fly={{ y: 200 }}>
		<slot name="header" />
		<slot />
		<slot name="footer" />
	</div>
</div>

<style>
	.modal-container {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: rgba(0, 0, 0, 0.7);
		z-index: 2;
	}

	.modal-content {
		background: var(--mainWhite);
		width: 85vw;
		max-width: 35rem;
		margin: 0 auto;
		margin-top: 5rem;
		padding: 3rem;
		border-radius: var(--mainBorderRadius);
		position: relative;
	}

	.modal-content .expense-form {
		box-shadow: none;
	}

	.modal-container .form {
		margin-bottom: 0;
	}

	.modal-container .expense-form {
		padding: 1.25rem 0;
	}

	.modal-container .form {
		position: static;
	}

	.modal-container .close-btn {
		top: 2%;
		right: 3%;
	}
</style>
