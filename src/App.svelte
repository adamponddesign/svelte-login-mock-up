<script>
	import LoginForm from './components/LoginForm.svelte';

	let navVariable = 'login-form'

	const updateProgressStatus = () => {
		navVariable = 'logged-in'
	}

</script>




<header>
	<img id="beyonk-logo" src="images/beyonk-logo.svg" alt="beyonk logo">
</header>

<main>

	{#if navVariable === 'login-form'}

		<div  class='form-container'>
			<div class='form-column left'>
				<img id="avatar" src="images/avatar-icon.svg" alt="generic avatar icon">
			</div>
			<div class='form-column right'>
				<LoginForm on:success={updateProgressStatus}/>
			</div>	
		</div>

	{:else}

		<div class='form-container success toUpperCase'>
			<img id="success-tick" src="images/success-tick.svg" alt="green tick image">
			Logged In!
		</div>

	{/if}

</main>



<style>
	header {
		height: 4rem;
		background: #32B0A2;
		-webkit-box-shadow: 9px 9px 15px -8px rgba(166,151,166,0.38);
		-moz-box-shadow: 9px 9px 15px -8px rgba(166,151,166,0.38);
		box-shadow: 9px 9px 15px -8px rgba(166,151,166,0.38);
	}


	main {
		display: flex;
		align-items: center;
		justify-content: center;
		height: calc(100vh - 4rem);
	}
	
	#avatar {
		fill:none;
		stroke:#303030;
		stroke-width:0.7;
		stroke-linecap:round;
		stroke-linejoin:round;
		stroke-miterlimit:10;
	}

	#beyonk-logo {
		width: 104px;
		fill: #000;
		padding: 0.85rem;
	}

	#success-tick {
		width: 8rem;
		height: 8rem;
		padding: 1rem;
	}


	.form-container {
		display: flex;
		background-color: #f5f5f5;
		width: 50vw;		/* 50% of screen width as per brief*/
		height: 60vh;		/* 60% of screen height as per brief*/
		border-radius: 10px;
		-webkit-box-shadow: 9px 9px 15px -8px rgba(166,151,166,0.38);
		-moz-box-shadow: 9px 9px 15px -8px rgba(166,151,166,0.38);
		box-shadow: 9px 9px 15px -8px rgba(166,151,166,0.38);
	}

	.form-container.success {
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}

	.form-column {
		padding: 1rem;
		width: 50%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}


</style>

