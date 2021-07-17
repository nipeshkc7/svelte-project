<script>
	import { onMount } from "svelte";
	import { apiData, drinkNames } from './store.js';
	export let name;

	onMount(async () => {
		fetch(
			"https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=Bourbon"
		)
			.then((response) => response.json())
			.then((data) => {
				console.log(data);
				apiData.set(data);
			})
			.catch((error) => {
				console.log(error);
				return [];
			});
	});
</script>

<main>
	<div class="intro"> 
	<h1>Hello {name}!</h1>
	<p>Welcome to my first svelte project !</p>
	<p><b>Look how I make an amazing API call:</b></p>
	</div> 
	<div>
		<ul>
			{#each $drinkNames as drinkName}
				<li>{drinkName}</li>
			{/each}
			</ul>
	</div>

</main>

<style>
	.intro {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
