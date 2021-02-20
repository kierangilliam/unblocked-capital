<script lang='ts'>
    import { fetchNotion } from '@leveluptuts/svelte-notion';
    import { Notion } from '../../components'
    import { metatags, goto, params } from '@roxi/routify'


    $: notionData = $params && (async () => {
        return await fetchNotion({ id: $params.id, context: this })
    })()

    const gotoPage = (id: string) => () => {
        $goto(`./post/${id}`)
    }

    metatags.title = 'Unblocked Captial'
    metatags.description = 'Learn to code for algorithmic trading'
</script>

{#await notionData}
    <p>...waiting</p>
{:then blocks}
    <Notion {blocks} {gotoPage} />
{:catch error}
    <p>An error occurred!</p>
{/await}