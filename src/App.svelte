<script>
	import NavBar from "./components/navbar.svelte";
	import Footer from "./components/Footer.svelte";
	import HomePage from "./components/Home.svelte";
	import Contact from "./components/Contact.svelte";
	import Reader from "./components/main.svelte";
	let Page = "home";
	let code = "(9701)/2001/9701_w01_qp_3.pdf";
	let address_qp =
		"http://localhost:5000/file?address=(9701)/2001/9701_w01_qp_3.pdf";
	let address_ms =
		"http://localhost:5000/file?address=(9701)/2001/9701_w01_ms_3.pdf";
	const clickhandle = () => {
		address_qp = "http://localhost:5000/file?address=" + code;
		address_ms = addr_qp.replace("qp", "ms");
		alert(code);
	};
</script>

<main>
	<NavBar bind:Page />
	{#if Page == "home"}
		<HomePage bind:Page />
	{:else if Page == "contact"}
		<Contact />
	{:else if Page == "viewer"}
		<input bind:value={code} />
		<button on:click={clickhandle}>click</button>
		{#key address_qp}
			<Reader addr_qp={address_qp} addr_ms={address_ms} />
		{/key}
	{:else}
		<div>
			<h1>404</h1>
			<p>Page not found</p>
		</div>
	{/if}
	<Footer />
</main>
