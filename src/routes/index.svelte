<script context="module">
	import axios from "axios";
	export const prerender = true;
	
</script>

<script>
	import Counter from "$lib/Counter.svelte";
	import { onMount } from "svelte";

	let message = "test";
	let user = {}
	onMount(async () => {
		// const response = await fetch("http://localhost:44314/api/User/current", {
		// 	headers: { "Content-Type": "application/json" },
		// 	credentials: "include",
		// });
		// const content = await response.json();
		// debugger;
		// console.log(content);

		const url = "http://localhost:44314/api/User/current";
		const token = localStorage.getItem("t");
		if (token != null) {
			const config = {
				headers: {
					Authorization: `Bearer ${token}`,
				},
			};
			debugger;
			axios
				.get(url, config)
				.then(function (response) {
					let data = response.data;
					console.log(data);
					user = data;
				})
				.catch(function (error) {});
		} else {
			//not authorised
		}
	});
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	Hello {user.firstname} {message}
	<h1>
		<span class="welcome">
			<picture>
				<source srcset="svelte-welcome.webp" type="image/webp" />
				<img src="svelte-welcome.png" alt="Welcome" />
			</picture>
		</span>

		to your new<br />SvelteKit app
	</h1>

	<Counter />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
