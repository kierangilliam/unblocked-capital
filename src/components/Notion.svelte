<script>
    import { url } from '@roxi/routify'
    import Blocks from './blocks/Blocks.svelte'
    import EmailForm from './EmailForm.svelte'

    export let blocks
    export let gotoPage
    
    $: title = blocks[0]
    $: pageBlocks = blocks.slice(1)
        // WIP blocks are prefaced with 'RM'
        .filter(b => {
            let content = b?.properties?.title ?? []

            if (content[0] && content[0][0]) {
                return content[0][0].startsWith('RM') === false
            }

            return true
        })

    $: emailSplitIndex = nthOf(pageBlocks, 4, b => b.type === 'text')
    $: blocksBefore = pageBlocks.slice(0, emailSplitIndex)
    $: blocksAfter = pageBlocks.slice(emailSplitIndex)

    const nthOf = (list, n, cb) => {
        let index = 0
        let result = 0
        for (let i = 0; i < n; i++) {
            index = list.slice(result).findIndex(cb)
            result += index + 1
        }
        return result
    }
</script>

<div class='title'>
    <h1>{title.properties.title[0][0]}</h1>
    {#if $url() !== ''}
        <a href='{$url('/')}'>Home</a>
    {/if}
</div>


{#if pageBlocks.length > 0}
    <Blocks blocks={blocksBefore} {gotoPage} />
    <EmailForm />
    <Blocks blocks={blocksAfter} {gotoPage} />
{:else}
    <div>
        Nothing here yet... come back soon
    </div>
    <a href='/'>Home</a>
{/if}

<style>
    .title {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>