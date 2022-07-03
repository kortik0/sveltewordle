<script>
    import logo from './assets/svelte.png'
    import {onMount} from 'svelte'

    let element
    let arrOfElement
    let currentCollection

    let isWin = undefined

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

    let isEnd = false
    $: randomedWord = words[Math.floor(Math.random() * words.length)]

    const createPelement = (value) => {
        const element = document.createElement('p');
        element.textContent = value
        return element
    }

    onMount(() => {
        arrOfElement = Array.from(element.children).map(child => {
            return Array.from(child.children)
        })

        currentCollection = arrOfElement.shift()
    })

    const logic = (evt) => {
        console.log(evt)

        if (evt.key === "Enter") {
            const length = currentCollection.reduce((currentAcc, block) => {
                return currentAcc += block.classList.contains('done') ? 1 : 0
            }, 0)

            if (length === 6) {
                let rightCount = 0
                currentCollection.forEach((block, index) => {
                    const textContent = block.children[0].textContent;
                    if (textContent === randomedWord[index]) {
                        console.log(index, "is right")
                        block.style = "background: green!important"
                        rightCount++
                    }

                    if (textContent !== randomedWord[index] && randomedWord.includes(textContent)) {
                        console.log(index, 'right but wrong position')
                        block.style = "background: yellow!important"
                    }
                })

                if (rightCount === length) {
                    isWin = true
                    isEnd = true
                    document.removeEventListener('keyup', logic)
                }

                if (arrOfElement.length === 0) {
                    isWin = false
                    isEnd = true
                    document.removeEventListener('keyup', logic)
                    return
                }

                rightCount = 0
                currentCollection = arrOfElement.shift()
            }
            return
        }

        if (evt.code.startsWith("Digit")) {
            return
        }

        if (evt.which >= 112 && evt.which <= 123) {
            evt.preventDefault()
            console.log(`Was clicked function key which ${evt.key}`)
            return
        }

        if (evt.key === "Alt" || evt.key === "Escape" || evt.key === "Shift" || evt.key === "Tab" || evt.key === "Control") {
            return
        }

        if (evt.key === "Backspace") {
            currentCollection.forEach(block => {
                if (block.classList.contains('done')) {
                    block.classList.remove("done")
                    block.removeChild(block.children[0])
                }
            })
            return;
        }

        for (let i = 0; i < currentCollection.length; i++) {
            if (!currentCollection[i].classList.contains('done')) {
                currentCollection[i].append(createPelement(evt.key))
                currentCollection[i].classList.add('done')
                return
            }
        }

        console.log(element)
        console.log(arrOfElement)
    }

    document.addEventListener("keyup", logic)
</script>

<main>
    <img src={logo} alt="Svelte Logo"/>
    <h1>Hello wordle!</h1>
    {#if isEnd}
        <h3 style="color: #f1f1f4">You {isWin ? "Win! 😎" : "Lose 😥"}</h3>
    {/if}
    <!--<p>randomed word: <span style="color: aqua">{randomedWord}</span></p>-->

    <div class="container" bind:this={element}>
        <div class="row">
            <div class="box">

            </div>
            <div class="box">

            </div>
            <div class="box">

            </div>
            <div class="box">

            </div>
            <div class="box">

            </div>
            <div class="box">

            </div>
        </div>
        <div class="row">
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
        </div>
        <div class="row">
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
        </div>
        <div class="row">
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
        </div>
        <div class="row">
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
        </div>
        <div class="row">
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
            <div class="box"></div>
        </div>
    </div>
</main>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .box {
        text-align: center;
        width: 50px;
        height: 50px;

        margin: 2px;

        background: #2f9fb4;
    }

    .row {
        display: flex;
        flex-direction: row;
        max-width: 640px;
    }

    .container {
        display: grid;
        justify-content: center;
        grid-template-rows: repeat(6, 1fr) minmax(1fr, 5fr);
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

    p {
        color: #f1f1f4;
        max-width: 14rem;
        margin: 1rem auto;
        line-height: 1.35;
    }

    @media (min-width: 480px) {
        h1 {
            max-width: none;
        }

        p {
            max-width: none;
        }
    }
</style>
