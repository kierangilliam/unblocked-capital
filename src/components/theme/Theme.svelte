<script lang='ts'>
    import { Theme } from '@ollopa/cedar'
    import { onMount } from 'svelte'

    const BASE = {
        white: '#FAFAFA',
        trueWhite: '#FFFFFF',
        black: '#181818',
        trueBlack: '#000000',

        lighterGray: '#F1F0F2',
        lightGray: '#D9D7E0',
        gray: '#C0BEC6',
        darkGray: '#646468',
        darkerGray: '#363638',

        lightRed: '#DE7272',
        red: '#FE785A',
        redText: '#FF5555',

        lightBlue: '#CFEEFF',
        blue: '#8ED7FF',
        darkBlue: '#069BEC',

        lightGreen: '#DDF3E3',
        green: '#AEE2BC',
        darkGreen: '#70CB89',

        gold: '#FFE6B5',
        purple: '#C1C8FF',
    }

    const ELEMENT_COLORS = {
        background: BASE.trueWhite,
        blockBg: '#F9F9F9',
        contextMenuBg: BASE.gray,
    }

    const COLORS = {
        ...BASE,
        ...ELEMENT_COLORS,

        danger: BASE.red,
        textColor: BASE.black,
        buttonColor: BASE.blue,
        selectedColor: BASE.darkBlue,

        lineColor: BASE.trueBlack,
        lightLineColor: BASE.black,
    }

    const setCSSVar = (element = document.documentElement) => ([name, value]: [string, string]) =>
        element.style.setProperty(`--${name}`, value)

    const getCSSVar = (name: string) =>
        getComputedStyle(document.body).getPropertyValue(`--${name}`)

    let themeRoot: HTMLElement

    onMount(() => Object.entries(COLORS).forEach(setCSSVar(themeRoot)))
</script>

<Theme>
    <div class='theme' bind:this={themeRoot}>
        <slot />
    </div>
</Theme>

<style>
    :global(*) {
        font-family: var(--bodyFont);   
    }
    :global(.theme) {
        /* Colors (defined using js) */
        --white: unset;
        --lightGray: unset;
        --darkGray: unset;
        --red: unset;
        --orange: unset;
        --lightOrange: unset;
        /* Color intetntions (defined using js) */
        --danger: unset;
        --background: unset;
        --textColor: unset;
        --buttonColor: unset;
		--selectedColor: unset;
        --lineColor: unset;
        --buttonTextColor: var(--darkOrange);
        --buttonWarnTextColor: var(--black);
        
        /* Borders */
        --borderRadius: 16px;
        --borderRadiusSmall: 12px;
        --borderRadiusFull: 999px;
        --buttonBorderRadius: var(--borderRadiusFull);
        --line: 1.5px solid var(--lineColor);
        --lineThin: 1px solid var(--lightLineColor);
        --hairline: 1px solid lightgrey;
        
        /* Typography */
        --headingFont: 'Alegreya', serif;
        --bodyFont: 'Alegreya', serif;
        --monoFont: 'IBM Plex Mono', monospace;   
        --medium: 500;
        --bold: 600;
     
        /* Minor Third */        
        --h1: 1.802rem;
        --h2: 1.602rem;
        --h3: 1.424rem;
        --h4: 1.266rem;
        --h5: 1.125rem;
        --textSmall: 0.889rem;
        /* View Paddings */
        --viewPaddingModal: var(--s-16);
        /* Component sizes */
        --toolbarHeight: 3rem;
		/* Z indices */
		--pinnedConnectionZ: 100;
    }    
    :global(.mono) { font-family: var(--monoFont); }
    :global(.bold) { font-weight: bold; }
    :global(.small) { font-size: var(--textSmall); }
    :global(.underline) { text-decoration: underline; }
</style>