<script>
	import { onMount } from 'svelte';

	let ethStore;
	let web3;
    let selectedAccount;
    let connected;
	
	onMount(async () => {
		const module = await import('sapper-web3');
		ethStore = module.ethStore;
		web3 = module.web3;
		selectedAccount = module.selectedAccount;
		connected = module.connected;
	});

	const enableBrowser = async () => {
        	await ethStore.setBrowserProvider();
    	}
</script>

<button on:click={enableBrowser}>Enable Browser</button>
