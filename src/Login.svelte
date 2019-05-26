<script>
	let email = '';
	let password = '';
	let messages = [];

	$: messages = [...verifyEmail(email), ...verifyPassword(password)];

	$: formIsValid = messages.length === 0;

	function verifyEmail() {
		let messages = [];
		if (email === '') {
			messages.push('Email must be given.');
		}
		return messages;
	}

	function verifyPassword() {
		let messages = [];
		if (password.length < 8) {
			messages.push('Password must have at least 8 characters.');
		}
		return messages;
	}

	export function doSignin() {
		doAction('signin');
	}

	export function doSignup() {
		doAction('signup');
	}

	function doAction(action) {
		if (formIsValid) {
			browser.runtime.sendMessage({
				action,
				email,
				password
			});
		}
	}
</script>

<main>	
	<h2>Login</h2>

	<label>Email</label>
	<input bind:value={email}>
	<label>Password</label>
	<input bind:value={password}>

	<button on:click={doSignin}>Sign In</button>
	<button on:click={doSignup}>Create Account</button>

	{#each messages as message}
		<p>{message}</p>
	{/each}
</main>