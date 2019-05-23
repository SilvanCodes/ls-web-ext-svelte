<script>
	import { onMount } from 'svelte';
	// custom components
	import Register from './Register.svelte';
	import Login from './Login.svelte';
	import Workspace from './Workspace.svelte';
	
	let user;
	let page = 'register';

	onMount(() => {
		browser.runtime.sendMessage({
			action: 'user'
		}).then(current => {
			user = current;
		});
	});

	// ACTION HANDLER
	browser.runtime.onMessage.addListener((message) => {
		console.log('app got message:', message)
		switch(message.action) {
		case 'user':
			user = message.user;
			break;
		default:
			console.warn('Action not implemented in app!')
		}
	});

	// NAVIGATION HANDLER
	function handleNavigation(event) {
		page = event.detail;
	}

</script>

<main>
	{#if user}
		<Workspace {...user} />
	{:else if page === 'login'}
		<Login on:navigate={handleNavigation}/>
	{:else if page === 'register'}
		<Register on:navigate={handleNavigation}/>
	{/if}
</main>