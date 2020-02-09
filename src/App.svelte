<script>
	import LoginForm from './components/LoginForm.svelte';

</script>




<main>
	<div class='form-container'>
		<div class='form-column left'>
			<img src="https://picsum.photos/seed/picsum/200/300" alt="mountains">
		
		</div>

		<div class='form-column right'>
			<LoginForm />
		</div>
	
	
	</div>
	
</main>



<style>
	main {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 100vh;
	}

	.form-container {
		display: flex;
		background-color: #fafafa;
		width: 50vw;
		height: 60vh;
	}

	.form-column {
		width: 50%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}


</style>

