<script>
    export let block
</script>

{#if block.properties}
    <p>
        {#each block.properties.title as items}
            {#if items.length > 1}
                {#if items[1][0][0] !== "a"}    
                    <span class={items[1][0].join(" ")}>{items[0]}</span>
                {:else}
                    <a href={items[1][0][1]} target="_blank" rel="noopener">
                        {items[0]}
                    </a>
                {/if}
            {:else}{items[0]}{/if}
        {/each}
    </p>
{:else}
    <br />
{/if}

<style>
    /* todo add more */
    :global(.i) {
        font-style: italic;
    }
    :global(.b) {
        font-weight: bold;
    }
</style>