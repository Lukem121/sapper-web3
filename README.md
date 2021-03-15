---

# Sapper-Web3 🌟

web3.js as a Svelte store that can be used in sapper.

## Installation

```bash
npm i sapper-web3
```

Include web3 in your template.html file
```bash
<script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
```

## Basic Usage

```js
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

<h2>{$selectedAccount}</h2>
<button on:click={enableBrowser}>Enable Browser</button>
```

To enable connection to the current window provider: 

```js
ethStore.setBrowserProvider()
```

To enable connection using an url string: 

```js
ethStore.setProvider('<ws/https or http provider url>')
```

If connection is successful, you can access the instantiated web3.js with the current window provider
using the `$` svelte store syntax :

```js
$web3.eth.getBalance(<Ethereum address>)
```

## Derived stores

* connected: true if connection to the provider was successful.
* chainId: The current blokchain Id.
* chainName: Name of the The current blokchain.
* selectedAccount: current selected account.
* nativeCurrency: currency name in the current chain.

Svelte stores are automatically updated when network or the selected account change.

Please see the file `example/index.svelte` for more usage information to start a transaction
and concrete usage of stores.
