<script>
	import Reader from "./main.svelte";

	var page = "subject";
	export let subject = "";
	export let year = "";
	export let id = "";
	const changePage = (pg) => {
		page = pg;
	};
	const getSubjects = async () => {
		const res = await fetch("http://localhost:5000/api?address=").then(
			(res) => res.json()
		);
		return res;
	};

	const getYears = async (subject) => {
		const res = await fetch(
			`http://localhost:5000/api?address=${subject}`
		).then((res) => res.json());
		return res;
	};
	const getPaper = async (subject, year) => {
		const res = await fetch(
			`http://localhost:5000/api?address=${subject}/${year}`
		).then((res) => res.json());
		return res;
	};

	const PrevClickH = () => {
		if (page == "year") {
			changePage("subject");
		} else if (page == "paper") {
			changePage("year");
		} else if (page == "reader") {
			changePage("paper");
		}
	};
</script>

<main>
	<button on:click={PrevClickH} class="pre">Previous</button>
	<br />

	{#if page == "subject"}
		<div>
			<p class="sub-intro">Choose a subject:</p>
			{#await getSubjects() then data}
				{#each data as sub}
					<button
						on:click={() => {
							changePage("year");
							subject = sub;
						}}>{sub}</button
					>
				{/each}
			{:catch error}
				{error}
			{/await}
		</div>
	{:else if page == "year"}
		<div>
			{#await getYears(subject) then data}
				{#each data as sub}
					<button
						on:click={() => {
							changePage("paper");
							year = sub;
						}}>{sub}</button
					>
				{/each}
			{:catch error}
				{error}
			{/await}
		</div>
	{:else if page == "paper"}
		<div>
			{#await getPaper(subject, year) then data}
				{#each data as sub}
					{#if sub.toString().includes("qp")}
						<button
							on:click={() => {
								id = sub;
								changePage("reader");
							}}>{sub}</button
						>
					{/if}
				{/each}
			{:catch error}
				{error}
			{/await}
		</div>
	{:else if page == "reader"}
		<!-- main reader -->
		<Reader {subject} {year} {id} />

	{:else}
		<div>
			<h1>404</h1>
			<p>Page not found</p>
		</div>
	{/if}
</main>

<style>
	div {
		padding: 10px;
	}
	button {
		text-decoration: none;
		display: inline-block;
		padding: 8px 16px;
	}

	button:hover {
		background-color: #ddd;
		color: black;
	}

	.pre {
		background-color: #ffad60;
		color: white;
	}
</style>
