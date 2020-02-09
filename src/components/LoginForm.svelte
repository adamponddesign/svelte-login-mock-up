<script>
    import { onMount } from 'svelte';
  

    let email;
	let password;
	let typingTimer;                //timer identifier
	let finishedTypingInterval = 3000;  //time in ms (3 seconds)
    let emailInputRef;	// for .focus() onMount and if validation fails
    let emailError;
    
    
    const emailRegex = RegExp( /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/ )     // email regex test

    // remove error message if field empty
    $: if (!email) {
        emailError = '';
    }


	onMount(() => {
        emailInputRef.focus()	// focus email input on page load
    });


	const typeTimer = () => {
		clearTimeout(typingTimer); 	//reset the timer on keyup
		if (email) {		// if email exists
			typingTimer = setTimeout(() => checkEmail(email), finishedTypingInterval);	// run the 'checkEmail' function after the 'finishedTypingInterval' amount of time
		}

	}
	const checkEmail = (email) => {
        console.log('checking email')
	    if (!emailRegex.test(email)) {
            console.log('email failed')
            emailInputRef.focus() 	// refocus on email input if validation failed
            emailError = 'Please enter a valid email address'
        } else {
            console.log('email passed')
            emailError = ''
        }
        
	}

</script>



	<form>
	
		<input bind:this={emailInputRef} on:blur={() => checkEmail(email)} on:keyup={typeTimer} bind:value={email} placeholder="enter email" type='email'>
        {#if emailError}
            <div>{emailError}</div>
        {/if}

		<input autocomplete="off" bind:value={password} placeholder="enter password" type='password'>
	
	
	</form>