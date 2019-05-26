<script>
	import { onMount } from 'svelte';
	// custom components
	import Login from './Login.svelte';
	import Workspace from './Workspace.svelte';
	
	let user;
	let errors = [];

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
		case 'error':
			console.log(message.error)
			errors = [ /* ...errors,  */message.error.message ];
			break;
		default:
			console.warn('Action not implemented in app!')
		}
	});

</script>

<main>
	{#if user}
		<Workspace {...user} />
	{:else}
		<Login/>
	{/if}
	<!-- {#each errors as error}
		<p>{error}</p>
	{/each} -->
</main>