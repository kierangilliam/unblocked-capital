<script lang='ts'>
    import { fetchNotion } from '@leveluptuts/svelte-notion';
    import { Notion } from '../components'
    import { metatags, goto } from '@roxi/routify'

    const notionData = (async () => {
        const pageId = '2a42fe43d6cf4b5db39ba0ed6dd1be0d'
        return await fetchNotion({ id: pageId, context: this })
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