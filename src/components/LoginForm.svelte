<script>
    import { onMount } from 'svelte';
  

    let email;
	let password;
	let typingTimer;                //timer identifier
	let finishedTypingInterval = 3000;  //time in ms (3 seconds)
    let emailInputRef;	// for .focus() onMount and if validation fails
    let passwordInputRef;
    let emailError;
    let passwordError;
    let valid = true;
    
    const emailRegex = RegExp( /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/ )     // email regex test
    const passwordRegex = RegExp( /^.{9,}$/ )

    // remove error message if field empty
    $: if (!email || !password) {
        emailError = '';
        passwordError = '';
    }


	onMount(() => {
        emailInputRef.focus()	// focus email input on page load
    });


	const typeTimer = () => {
		clearTimeout(typingTimer); 	//reset the timer on keyup
		if (email && !password) {		// if email exists
			typingTimer = setTimeout(() => checkEmail(email), finishedTypingInterval);	// run the 'checkEmail' function after the 'finishedTypingInterval' amount of time
        }
        if (password) {
            typingTimer = setTimeout(() => checkPassword(password), finishedTypingInterval);	// run the 'checkEmail' function after the 'finishedTypingInterval' amount of time
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
	const checkPassword = (password) => {
        console.log('checking password')
	    if (!passwordRegex.test(password)) {
            console.log('password failed')
            passwordInputRef.focus() 	// refocus on email input if validation failed
            passwordError = 'Please enter a valid password - must be more than 8 characters'
        } else {
            console.log('password passed')
            passwordError = ''
            valid = false;
        }
        
	}

</script>



	<form>
	
		<input bind:this={emailInputRef} on:blur={() => checkEmail(email)} on:keyup={typeTimer} bind:value={email} placeholder="enter email" type='email'>
        {#if emailError}
            <div>{emailError}</div>
        {/if}

		<input bind:this={passwordInputRef} autocomplete="off"  on:focusout={() => checkPassword(password)} on:keyup={typeTimer} bind:value={password} placeholder="enter password" type='password'>
         {#if passwordError}
            <div>{passwordError}</div>
        {/if}

        <button on:click|preventDefault={() => console.log('login successful')} disabled={valid}>Login</button>

	
	</form>