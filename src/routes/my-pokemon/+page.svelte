<script lang="ts">
    import { caughtMonsters } from "$lib/stores";
    import Monster from "../Monster.svelte";
</script>

<h2>My Pokémon</h2>

<div class="monsters">
    {#if $caughtMonsters.length > 0}
        {#each $caughtMonsters as monster}
        <Monster {monster} />
        {/each}
    {:else}
    <p>You haven't caught any Pokémon yet.</p>
    {/if}
</div>

<style>
    .monsters {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
    }
</style>
