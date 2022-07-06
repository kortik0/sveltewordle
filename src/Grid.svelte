<script>
    import {onMount} from "svelte";

    export let isWin;
    export let isEnd;
    export let randomedWord

    let element
    let arrOfElement;
    let currentCollection;

    onMount(() => {
        arrOfElement = Array.from(element.children).map(child => {
            return Array.from(child.children)
        })

        currentCollection = arrOfElement.shift()
        document.addEventListener("keyup", logic)
    })

    const createPelement = (value) => {
        const element = document.createElement('p');
        element.textContent = value
        return element
    }

    const checkIsRight = () => {
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

        if (rightCount === 6) {
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

        currentCollection = arrOfElement.shift()
    }

    const isPreventable = (evt) => {
        if (evt.which >= 112 && evt.which <= 123) {
            console.log(`Was clicked function key which ${evt.key}`)
            console.log("What are you looking for? 👀")
            return true
        }

        if (evt.code.startsWith("Digit") || evt.key === "Alt" || evt.key === "Shift" ||
            evt.key === "Escape" || evt.key === "Tab" ||
            evt.key === "Control" || evt.code === "Space"
        ) {
            return true
        }

        return false
    }

    const logic = (evt) => {
        if (isPreventable(evt)) {
            return
        }

        if (evt.key === "Enter") {
            const length = currentCollection.reduce((currentAcc, block) => {
                return currentAcc += block.classList.contains('done') ? 1 : 0
            }, 0)

            if (length === 6) {
                checkIsRight()
            }
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
    }
</script>

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

<style>
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
</style>