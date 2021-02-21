<script lang='ts'>
    import { Router } from '@roxi/routify'
    import { routes } from '../.routify/routes'
    import { Theme } from './components'
</script>

<Theme>
    <div class='wrapper'>
        <div class='title'>
            <h3 on:click={() => window.location.href = '/'}>Unblocked Captial</h3>
            <h5>Learning to code for algorithmic trading from scratch.</h5>
        </div>
        <div class='container'>
            <Router {routes} />
        </div>
    </div>
</Theme>

<style>
    @import '../assets/global.css';

    :global(h1, h2, h3, h4, h5, .page-link) {
        margin-top: var(--s-4) !important;
        margin-bottom: var(--s-4) !important;
    }
    :global(p) {
        margin-bottom: var(--s-3);
        line-height: var(--s-8);
    }
    :global(.page-link) {
        font-weight: bold;
        padding: var(--s-2) var(--s-3);
        border: 3px solid var(--darkBlue);
        box-shadow: var(--level-1);
        cursor: pointer;
    }
    :global(.page-link:hover) {
        box-shadow: var(--level-2);
    }
    .wrapper {
        font-size: 18px;
    }
     
    .title {
        margin-top: var(--s-6) !important;
        margin-bottom: var(--s-8) !important;
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 60vw;
        min-width: 400px;
        border-bottom: 2px solid var(--darkGray);
    }

    .wrapper {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    /* small screens */
    @media only screen and (max-width: 700px) {
        .wrapper {
            align-items: initial;
            padding: 0 var(--s-3); 
        }

        .title {
            flex-direction: column;
            align-items: flex-start;
            width: 100vw;
            min-width: 0;
        }
    }

    .container {
        max-width: 40rem;
    }
</style>