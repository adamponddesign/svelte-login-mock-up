<script>
    import { onMount } from 'svelte';
  

    let email;
	let password = '';
	let typingTimer;                //timer identifier
	let finishedTypingInterval = 3000;  //time in ms (3 seconds)
    let emailInputRef;	// for .focus() onMount and if validation fails
    let passwordInputRef;
    let emailError;
    let passwordError;
    let valid = true;
    let userEmail = 'test+1234@example.net'
    let userPassword = 'Test1234!'

    
     // email/password regex tests
    const emailRegex = RegExp( /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/ )
    const passwordRegex = RegExp( /^.{9,}$/ )

    // remove error messages if fields empty
    $: if (!email || !password) {
        emailError = '';
        passwordError = '';
    }


	onMount(() => {
        emailInputRef.focus()	// focus email input on page load
    });


	const typeTimer = (event) => {
		clearTimeout(typingTimer); 	//reset the timer on keyup
        if (email && !password) {		// if email exists
            if (event.keyCode === 13) {
                checkEmail(email)
            }
			typingTimer = setTimeout(() => checkEmail(email), finishedTypingInterval);	// run the 'checkEmail' function after the 'finishedTypingInterval' amount of time
        }
        if (password) {
            if (event.keyCode === 13) {
                checkPassword(password)
            }
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
            passwordInputRef.focus() 
        }
        
	}
	const checkPassword = (password) => {
        console.log('checking password')
	    if (!passwordRegex.test(password)) {
            console.log('password failed')
            passwordInputRef.focus() 	// refocus on email input if validation failed
            passwordError = 'Please enter a valid password - must be more than 8 characters'
            valid = true;
        } else if (passwordRegex.test(password)){
            console.log('password passed')
            passwordError = ''
            valid = false;
        }
    }
    
    const checkCredentials = () => {
        console.log('submit')

        if (email === userEmail && password === userPassword) {
            console.log('login successful')
        } else {
            console.log('user not found')
        }
    }

</script>


	<form on:submit|preventDefault={checkCredentials}>
        <h1>Member Login</h1>
	
		<input 
            autocomplete="on"  
            bind:this={emailInputRef} 
            on:blur={() => checkEmail(email)} 
            on:keyup={typeTimer}
            bind:value={email} 
            placeholder="enter email" 
            type='email'
            >

        {#if emailError}
            <div>{emailError}</div>
        {/if}




		<input 
            bind:this={passwordInputRef} 
            autocomplete="off"  
            on:blur={() => checkPassword(password)} 
            on:keyup={typeTimer} 
            bind:value={password} 
            placeholder="enter password" 
            type='password'
            >

         {#if passwordError}
            <div>{passwordError}</div>
        {/if}


        <button disabled={valid}>Login</button>
	
	</form>


    <style>
    
    form {
        display: flex;  
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    
    </style>