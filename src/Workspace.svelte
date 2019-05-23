<script>
    export let email;

    export function logout() {
		console.log('fire logout')
		browser.runtime.sendMessage({
			action: 'logout'
		});
	}
</script>

<main>
    <h2>Workspace</h2>

    <p>Hello {email}!</p>

    <button on:click={logout}>Logout</button>
</main>