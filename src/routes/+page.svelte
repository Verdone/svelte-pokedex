<script lang="ts">
import { goto } from '$app/navigation';
import { page } from '$app/stores';
import type { PageData } from './$types';
import type { IndexMonster } from './+page';
import Monster from './Monster.svelte';
import { generations } from './generations';

export let data: PageData;

let form = {
	searchString: '',
}

let searchString = '';
$: selectedMonsters = data.monsters.filter(monster => {
	return monster.name.toLowerCase().includes(searchString.toLowerCase());
});

$: selectedGenerationId = $page.url.searchParams.get('generation_id') || '';

const updateSearchParams = (key: string, value: string) => {
    const searchParams = new URLSearchParams($page.url.search);
    searchParams.set(key, value);
    goto(`?${searchParams.toString()}`);
};

const submitSearch = (e: Event) => {
	searchString = form.searchString;
};

</script>

<div class="generations">
	<button 
		class="generation"
		class:active={selectedGenerationId === 'all'}
		on:click={() => updateSearchParams('generation_id', 'all')}
	>
		All
	</button>
	{#each generations as generation (generation.id)}
		<button 
			class="generation"
			class:active={selectedGenerationId === generation.id.toString()}
			on:click={() => updateSearchParams('generation_id', generation.id.toString())}
		>
		 	{generation.main_region}
		</button>
	{/each}
</div>

<form class="search-form" on:submit|preventDefault={submitSearch}>
	<input class="search-field" type="text" bind:value={form.searchString} placeholder="Search for a Pokémon names" />
	<input type="submit" value="Search" />
</form>


<div class="monsters">
	{#each selectedMonsters as monster (monster.id)}
		<Monster
			monster={monster}
		/>
	{/each}
</div>

<style>
	.generations {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
	}
	.generation {
		margin: 5px;
		padding: 5px 10px;
		border: 1px solid #ccc;
		background-color: #eee;
		color: #333;
		cursor: pointer;
	}
	.generation.active {
		background-color: #333;
		color: #eee;
	}
	.generation:hover {
		background-color: #777777;
		color: #eee;
	}
	.generation.active:hover {
		background-color: #444;
	}
	.monsters {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
	}
	.search-field{
		padding: 5px 10px;
		border: 1px solid #333;
		border-radius: 5px;
		width: 200px;
	}
	.search-form {
		display: flex;
		justify-content: center;
		margin: 20px 0;
	}
	.search-form input[type="submit"] {
		margin-left: 10px;
		padding: 5px 10px;
		border: 1px solid #333;
		background-color: #eee;
		border-radius: 5px;
	}
	.search-form input[type="submit"]:hover {
		background-color: #ddd;
		cursor: pointer;
	}
</style>
