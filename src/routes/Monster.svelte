<script lang="ts">
	import type { IndexMonster } from "./+page";
	import { caughtMonsters } from "$lib/stores";

    export let monster: IndexMonster;
	
	const catchMonster = () => {
		caughtMonsters.update((monsters) => {
			return [...monsters, monster];
		});
		console.log("catch monster ", monster);
	}
</script>

<div class="monster">
    <div role="none" on:click={catchMonster}>
        <div class="monster-content">
            <img src={monster.image} alt={monster.name} />
            {monster.name}
        </div>
        <div class="monster-id">
            {monster.id}
        </div>
    </div>
</div>	

<style>
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