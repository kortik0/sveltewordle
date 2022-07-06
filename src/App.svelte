<script>
    import logo from './assets/svelte.png'
    import Grid from "./Grid.svelte";

    $: isWin = false
    $: isEnd = false

    const words = [
        "create",
        "credit",
        "crisis",
        "custom",
        "damage",
        "danger",
        "dealer",
        "debate",
        "decade",
        "decide",
        "defeat",
        "defend",
        "define",
        "degree",
        "demand",
        "depend",
        "deputy",
        "desert",
        "design",
        "desire",
        "detail",
        "detect",
        "device",
        "differ",
        "dinner",
        "direct",
        "doctor",
        "dollar",
        "domain",
        "double",
        "driven",
        "driver",
        "during",
        "easily",
        "eating",
        "editor",
        "effect",
        "effort",
        "eighth",
        "either",
        "eleven",
        "emerge",
        "empire",
        "employ",
        "enable",
        "ending",
        "energy",
        "engage",
        "engine",
        "enough",
        "ensure",
        "entire",
        "entity",
        "equity",
        "escape",
        "estate",
        "ethnic",
        "exceed",
        "except",
        "excess",
        "expand",
        "expect",
        "expert",
        "extend",
        "extent",
        "fabric",
        "facing",
        "factor",
        "failed",
        "fairly",
        "fallen",
        "family",
        "famous",
        "father",
        "fellow",
        "female",
        "figure",
        "filing",
        "finger",
        "finish",
        "fiscal",
        "flight",
        "flying",
        "follow",
        "forced",
        "forest",
        "forget",
        "formal",
        "format",
        "former",
        "foster",
        "fought",
        "fourth",
        "French",
        "friend",
        "future",
        "garden",
        "gather",
        "gender",
        "german",
        "global",
        "golden",
        "ground",
        "growth",
        "guilty",
        "handed",
        "handle",
        "happen",
        "hardly",
        "headed",
    ]
    $: randomedWord = words[Math.floor(Math.random() * words.length)]
</script>

<main>
    <img src={logo} alt="Svelte Logo"/>
    <h1>Hello wordle!</h1>
    {#if isEnd}
        <h3 style="color: #f1f1f4; margin-bottom: 30px">
            You {@html isWin ? "Win! 😎" : `Lose 😥! Word was <span style="color: #2f9fb4">${randomedWord}</span>`}
        </h3>
    {/if}
    <!--<p>randomed word: <span style="color: aqua">{randomedWord}</span></p>-->

    <Grid bind:isEnd bind:isWin bind:randomedWord/>
</main>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    :root {
        background: #1d2447;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
        Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }

    main {
        text-align: center;
        padding: 1em;
        margin: 0 auto;
    }

    img {
        height: 10rem;
        width: 10rem;
    }

    h1 {
        color: #f1f1f4;
        text-transform: uppercase;
        font-size: 4rem;
        font-weight: 100;
        line-height: 1.1;
        margin: 2rem auto;
        max-width: 14rem;
    }

    /*p {*/
    /*    color: #f1f1f4;*/
    /*    max-width: 14rem;*/
    /*    margin: 1rem auto;*/
    /*    line-height: 1.35;*/
    /*}*/

    @media (min-width: 480px) {
        h1 {
            max-width: none;
        }

        /*p {*/
        /*    max-width: none;*/
        /*}*/
    }
</style>
