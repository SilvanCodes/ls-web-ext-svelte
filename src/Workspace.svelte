<script>
    export let email;

    export function signout() {
		console.log('fire signout')
		browser.runtime.sendMessage({
			action: 'signout'
		});
	}
</script>

<main>
    <h2>Workspace</h2>

    <p>Hello {email}!</p>

    <button on:click={signout}>SIGN OUT</button>
</main>