<script>
    import Code from './Code.svelte'
    import Text from './Text.svelte'

    export let blocks
    export let gotoPage

    const title = (block) => {
        if (
            block?.properties?.title
            && block?.properties?.title[0]
            && block?.properties?.title[0][0]) {
            return block?.properties?.title[0][0]
        }
        return ''
    }
</script>

{#each blocks as block} 
    {#if block.type === 'header'}
        <h1>{title(block)}</h1>
    {:else if block.type === 'page'}
        <!-- Hacky but don't show main page -->
        {#if block.id !== '2a42fe43-d6cf-4b5d-b39b-a0ed6dd1be0d'}
            <div class='page-link' on:click={gotoPage(block.id)}>{block?.properties?.title[0][0]}</div>
        {/if}
    {:else if block.type === 'sub_header'}
        <h2>{title(block)}</h2>
    {:else if block.type === 'sub_sub_header'}
        <h3>{title(block)}</h3>
    {:else if block.type === 'numbered_list'}
        <li>{title(block)}</li>
    {:else if block.type === 'text'}
        <Text {block} />
    {:else if block.type === 'divider'}
        <hr />
    {:else if block.type === 'quote'}
        <blockquote class='notion-quote'>
            {title(block)}
        </blockquote>
    {:else if block.type === 'code'}
        <Code
            code={title(block)}
            lang={block.properties.language[0][0]} />
    <!-- {:else}
        {block.type} -->
    {/if}
{/each}

<style>
    .notion-quote {
        background: var(--lightGray);
        padding: var(--s-4);
    }
</style>