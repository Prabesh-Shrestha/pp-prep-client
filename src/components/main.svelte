<script>
	import PdfViewer from "svelte-pdf";
	export let subject;
	export let year;
	export let id;
	let ms = true;

	export let addr_qp =
		"http://localhost:5000/file?address=" + subject + "/" + year + "/" + id;
	export let addr_ms = addr_qp.replace("qp", "ms");
</script>

<main>
	<div>
		code: <span>{subject}/{year}/{id}</span>
	</div>
	<button on:click={() => (ms = !ms)} id="ms-button">Mark Scheme?</button>
	{#if ms}
		<PdfViewer url={addr_qp} align="left" />
	{:else}
		<PdfViewer url={addr_ms} align="right" />
	{/if}
</main>

<style>
	main {
		height: 40%;
	}
</style>
