<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let email = '';
	let password = '';

	export function navigate(page) {
		return () => dispatch('navigate', page);
	}

	export function signup() {
		console.log('fire signup')
		browser.runtime.sendMessage({
			action: 'signup',
			email,
			password
		});
	}
</script>

<main>
	<h2>Register</h2>

	<label>Email</label>
	<input bind:value={email}>
	<label>Password</label>
	<input bind:value={password}>

	<p>{email}</p>

	<button on:click={signup}>Register</button>
	<button on:click={navigate('login')}>Go to Login</button>
</main>