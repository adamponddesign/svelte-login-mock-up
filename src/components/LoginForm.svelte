<script>
    import { onMount } from 'svelte';
  

    let name;
	let password;
	let typingTimer;                //timer identifier
	let finishedTypingInterval = 3000;  //time in ms (3 seconds)
	let emailInputRef;	// for .focus() onMount and if validation fails



	onMount(() => {
        emailInputRef.focus()	// focus email input on page load
    });


	const typeTimer = () => {
		clearTimeout(typingTimer); 	//reset the timer on keyup
		if (name) {		// if name exists
			typingTimer = setTimeout(checkEmail, finishedTypingInterval);	// run the 'checkEmail' function after the 'finishedTypingInterval' amount of time
		}

	}
	const checkEmail = () => {
		console.log('checkEmail')
		emailInputRef.focus() 	// refocus on email input if validation failed
	}

</script>



	<form>
	
		<input bind:this={emailInputRef} on:blur={checkEmail} on:keyup={typeTimer} bind:value={name} placeholder="enter email" type='email'>

		<input autocomplete="off" bind:value={password} placeholder="enter password" type='password'>
	
	
	</form>