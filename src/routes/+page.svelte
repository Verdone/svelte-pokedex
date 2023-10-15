<script lang="ts">
import { goto } from '$app/navigation';
import { page } from '$app/stores';
import type { PageData } from './$types';
import type { IndexMonster } from './+page';
import { generations } from './generations';

export let data: PageData;

$: monsterId = $page.url.searchParams.get('monsterId') || '';
$: monster = data.monsters.find(monster => monster.id === monsterId);
$: monsterId2 = $page.url.searchParams.get('monsterId2') || '';
$: monster2 = data.monsters.find(monster => monster.id === monsterId2);

const updateSerachParams = (key: string, value: string) => {
    const searchParams = new URLSearchParams($page.url.search);
    searchParams.set(key, value);
    goto(`?${searchParams.toString()}`);
};

</script>

<h1>{monsterId}</h1>
<h2>{monster?.name}</h2>
<h1>{monsterId2}</h1>
<h2>{monster2?.name}</h2>

<div class="generations">
	{#each generations as generation (generation.id)}
		<div class="generation">{generation.main_region}</div>
	{/each}
</div>

<div class="monsters">
	{#each data.monsters as monster (monster.id)}
	<div class="monster">
        <div role="none" on:click={() => updateSerachParams('monsterId', monster.id)}>
			<div class="monster-content">
				<img src={monster.image} alt={monster.name} />
				{monster.name}
			</div>
			<div class="monster-id">
				{monster.id}
			</div>
		</div>
        <div role="none" on:click={() => updateSerachParams('monsterId2', monster.id)}>
            Add Monster 2
        </div>
    </div>	
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
	}
	.generation:hover {
		background-color: #ddd;
	}
	.monsters {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
	}
	.monster-id {
		position: absolute;
		top: 0;
		left: 0;
		font-size: 0.8em;
		color: #aaa;
	}
	.monster {
		width: 100px;
		margin: 5px;
		padding: 10px;
		position: relative;
		background-color: #eee;
	}
	.monster:hover {
		background-color: #ddd;
	}
	.monster-content {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>
