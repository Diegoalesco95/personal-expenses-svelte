<script>
	import Title from './Title.svelte';

	export let total = 0;
</script>

<section class="main-title">
	<Title title="Total Expenses: ${total}" />
</section>
