<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let email = '';
	let password = '';

	export function navigate(page) {
		return () => dispatch('navigate', page);
	}

	export function login() {
		console.log('fire login')
		browser.runtime.sendMessage({
			action: 'login',
			email,
			password
		});
	}
</script>

<main>
	<h2>Login</h2>

	<label>Email</label>
	<input bind:value={email}>
	<label>Password</label>
	<input bind:value={password}>

	<button on:click={login}>Login</button>
	<button on:click={navigate('register')}>Register</button>
</main>