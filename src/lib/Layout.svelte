<script lang="ts">
    import { flip } from 'svelte/animate';
    import { fly } from 'svelte/transition';
    import { quadOut } from 'svelte/easing';

    export let pi: string;
    export let index: number;

    function getRange(pi: string, index: number, spread: number): string[] {
        if (index < spread) {
            const arr = pi.slice(0, index + spread + 1).split('');
            return [...Array(spread - index).fill(''), ...arr];
        }

        return pi.slice(index - spread, index + spread + 1).split('');
    }

    const spread = 2;
    const width = 40;
    const duration = 200;

    $: range = getRange(pi, index, spread);
</script>

<div>
    {#each range as digit, i (index + i)}
        <p
            class:current={i === spread}
            style:width={width + 'px'}
            in:fly={{ x: width, easing: quadOut, duration }}
            out:fly={{ x: -width, easing: quadOut, duration }}
            animate:flip={{ easing: quadOut, duration }}
        >
            {digit}
        </p>
    {/each}
</div>

<style>
    div {
        display: flex;
        flex-direction: row;
        width: fit-content;
    }
    p {
        margin: 0;
        padding: 0;
        text-align: center;
        text-justify: center;

        font-size: 50px;
    }
    p.current {
        font-weight: bolder;
    }
</style>
