<script lang="ts">
    import Layout from '$lib/Layout.svelte';
    import { pi } from '$lib/constants';
    // const pi ='3.14159'
    import { fade } from 'svelte/transition';
    let index = 0;

    $: hasWon = index === pi.length;

    function handleKeydown({ key }: KeyboardEvent) {
        if (key === pi[index]) index++;
    }
</script>

<svelte:window on:keydown={handleKeydown} />

{#if !hasWon}
    <div transition:fade><Layout {pi} {index} /></div>
{:else}
    <h1 transition:fade={{delay: 1000}}>Nice job!!!</h1>
{/if}

<style>
    :global(body) {
        --color: #cdd6f4;
        --font: Roboto, sans-serif;
        background-color: #1e1e2e;
        color: var(--color);
        font-family: var(--font);
        margin: auto;
        width: 95%;
        height: 95vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>
