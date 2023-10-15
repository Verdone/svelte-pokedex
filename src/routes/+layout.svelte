<script lang="ts">
    import { page } from "$app/stores";
    import { caughtMonsters } from "$lib/stores";
</script>

<div class="navbar">
    <a href="/" class:active={$page.url.pathname == '/'}>Home</a>
    <a href="/my-pokemon" class:active={$page.url.pathname == '/my-pokemon'}>
        My Pokémon
        {#if $caughtMonsters.length > 0}
            ({$caughtMonsters.length})
        {/if}
    </a>
</div>

<div class="container">
    <slot />
</div>

<style>
    :global(body) {
        margin: 0;
        padding: 0;
    }

    .navbar {
        display: flex;
        justify-content: space-between;
        background-color: #333;
        color: #fff;
        padding: 10px;
    }
    .navbar a {
        text-decoration: none;
        color: #fff;
    }
    .navbar a:hover {
        color: #ccc;
    }
    .navbar a.active {
        border: 1px solid #ccc;
        border-radius: 4px;
    }


    .container {
        max-width: 90%;
        margin: 0 auto;
        width: 1200px;
    }
</style>