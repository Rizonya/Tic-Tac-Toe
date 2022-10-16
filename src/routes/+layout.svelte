<script>
	import './styles.css';
	import "../app.css";
</script>

<div class="app">
	<header class='text-3xl text-center py-2'  > Tic tac toe</header>
	<main>
		<slot />
	</main>
</div>

<style>
	header{

		font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans';
	}
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-items: center;
		justify-content: center;
		align-items: center;
		padding: 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

</style>