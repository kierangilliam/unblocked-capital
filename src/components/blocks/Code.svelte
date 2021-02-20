<script>
    // @import 'highlight.js/styles/github.css';
    import hljs from 'highlight.js'

    export let code
    export let lang

    const { value: highlighted } = hljs.highlight(lang, code)
    $: code = `<pre class='language-javascriptreact'><code>${highlighted}</code></pre>`
</script>

<div>
    {@html code}
</div>

<style>
    div {
        border: var(--line);
        border-radius: var(--borderRadius);
        padding: 0 var(--s-4);
        overflow-x: scroll;
    }
</style>
