<script>
    import Code from './blocks/Code.svelte'
    import Text from './blocks/Text.svelte'

    export let blocks
    export let gotoPage
    
    $: title = blocks[0]
    $: pageBlocks = blocks.slice(1)
</script>

<h1>{title.properties.title[0][0]}</h1>

{#each pageBlocks as block}
    {#if block.type === 'header'}
        <h1>{block.properties.title[0][0]}</h1>
    {:else if block.type === 'page'}
        <div class='page-link' on:click={gotoPage(block.id)}>{block.properties.title[0][0]}</div>
    {:else if block.type === 'sub_header'}
        <h2>{block.properties.title[0][0]}</h2>
    {:else if block.type === 'sub_sub_header'}
        <h3>{block.properties.title[0][0]}</h3>
    {:else if block.type === 'text'}
        <Text {block} />
    {:else if block.type === 'divider'}
        <hr />
    {:else if block.type === 'quote'}
        <blockquote class='notion-quote'>
            {block.properties.title[0][0]}
        </blockquote>
    {:else if block.type === 'code'}
        <Code
            code={block.properties.title[0][0]}
            lang={block.properties.language[0][0]} />
    <!-- {:else}
        {block.type} -->
    {/if}
{:else}
    <div>
        Nothing here yet... come back soon
    </div>
    <a href="/">Home</a>
{/each}