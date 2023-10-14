<script lang="ts">
import type { PageData } from "./$types";
import { generations } from "./generations";

export let data: PageData;

</script>

<div class="monsters">
    {#each data.monsters as monster (monster.id)}
        <img src="{monster.image}" alt="{monster.name}" srcset="">
        <div class="monster">{monster.id}: {monster.name}</div>
    {/each}
</div>

{#each generations as generation (generation.id)}
    <h1>{generation.name}</h1>
    <p>Games: {generation.games.join(', ')}</p>
    <p>Main Region: {generation.main_region}</p>
{/each}

<style>
.monsters {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}
.monster {
    height: 100px;
    width: 100px;
    border: 1px solid black;
    margin: 5px;
    padding: 10px;
}
</style>
