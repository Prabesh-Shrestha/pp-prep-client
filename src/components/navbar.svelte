<script>
	export var Page;
	const changePage = (page) => {
		Page = page;
	};
</script>

<main>
	<ul>
		<li>
			<a
				href="#home"
				on:click={() => {
					changePage("home");
				}}>Home</a
			>
		</li>
		<li>
			<a
				href="#contact"
				on:click={() => {
					changePage("viewer");
				}}>Viewer</a
			>
		</li>
		<li>
			<a
				href="#contact"
				on:click={() => {
					changePage("contact");
				}}>Contact</a
			>
		</li>
		<li style="float:right">
			<img
				src="https://mystickermania.com/cdn/stickers/anime/demon-slayer-nezuko-kamado-512x512.png"
				alt="sus"
				height="40"
			/>
		</li>
	</ul>
</main>

<style>
	ul {
		list-style-type: none;
		margin: 0;
		padding: 0;
		overflow: hidden;
		background-color: #333;
	}

	li {
		padding: 0;
		margin: 0;
		float: left;
	}

	li a {
		display: block;
		color: white;
		text-align: center;
		padding: 14px 16px;
		text-decoration: none;
	}

	li a:hover:not(.active) {
		background-color: #111;
	}

	/* .active {
		background-color: #04aa6d;
	} */
</style>
