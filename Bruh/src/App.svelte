<script>
    import { Clock } from "./clock";
    import { spring, tweened } from "svelte/motion";

    let clock = new Clock(18, 15);
    let i = 0;

    clock.alarm = "13:50";

    function tick() {
        clock.tick();
        clock = clock;
        i++;
    }
    setInterval(tick, 1000);
</script>

<main>
    <div class="gridthing">
        <div class="secondclock">
            <svg viewBox="-50 -50 100 100">
                <circle class="clock-face" r="48" />

                {#each [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55] as minutes}
                    <line
                        class="hour"
                        y1="40"
                        y2="45"
                        transform="rotate({30 * minutes})"
                    />

                    {#each [1, 2, 3, 4] as offset}
                        <line
                            class="hour"
                            y1="42"
                            y2="45"
                            transform="rotate({6 * (minutes + offset)})"
                        />
                    {/each}
                {/each}

                <line
                    class="hourHand"
                    y1="-2.5"
                    y2="28"
                    transform="rotate({180 + (6/12) * (clock.clockMinute + clock.clockHour * 60)})"
                />
                <line
                    class="minuteHand"
                    y1="-2.5"
                    y2="36.5"
                    transform="rotate({180 + 6 *  clock.clockMinute})"
                />
            </svg>
        </div>

        <div class="thirdclock">
            <h1 id="clock3">
                {clock.time}
            </h1>
        </div>

        <div class="firstclock">
                <div id="paBent">
                    <h1 id="clock1">
                        {clock.time}
                    </h1>
                    <img id="clockpicture" src="digitalclock.png" alt="digitalclockpicture">
                </div>
        </div>

        
        <div id="larm">
            <input class="laarmInput" bind:value={clock.alarm}>
            {#if clock.isTriggered}
                <div class="shake">
                    <p class="wkae">wkae up</p>
                </div>
            {/if}
        </div>
</main>

<style>
    :global(body) {
        background: rgb(255, 255, 255);
        background: linear-gradient(-50deg, rgba(0, 255, 170, 0.705) 0%, rgba(204, 0, 255, 0.507) 50%, rgba(255, 0, 85, 0.767) 100%), url(https://images2.alphacoders.com/685/thumb-1920-685487.jpg);
        background-repeat:no-repeat;
        background-attachment: fixed;
    }
    .gridthing{
        display: grid;
        grid-template-columns: repeat(3, auto);
        grid-template-rows: repeat(4, auto);
    }
    main {
        justify-content:space-evenly;
        flex-wrap: wrap; 
        text-align: center;
        align-items: center;
    }
    #clockpicture {
        width: 490px;
        z-index: -1;
    }
    @font-face{
        font-family:'digital-clock-font';
        src: url('./digital-dismay.regular.otf');
    }
    @font-face{
        font-family:'funny-font';
        src: url('./JMH Psychedelic CAPS.otf');
    }
    @keyframes ranibow {
        0%, 100% {transform: rotate(10deg); color: rgb(0, 255, 179);font-size: 8em}
        12.5%, 87.5% {transform: rotate(-10deg);color: rgb(91, 181, 255);font-size: 4em}
        25%, 75% {transform: rotate(10deg);color: rgb(255, 0, 140);font-size: 10em}
        37.5%, 62.5% {transform: rotate(-10deg);color: rgb(255, 108, 82);font-size: 12em}
        50% {transform: rotate(10deg);color: rgb(255, 174, 0);font-size: 2em}
    }
    @keyframes wakeUps {
        0%, 100% {transform: rotate(0deg); color: rgb(255, 0, 0);font-size: 3em}
        25%, 75% {transform: rotate(180deg); color: rgb(0, 255, 0);font-size: 1em}
        50%, 50% {transform: rotate(-180deg); color: rgb(0, 0, 255);font-size: 5em}
    }
    #clock1 {color: rgb(32, 32, 32);
        font-family: "digital-clock-font";
        font-size: 8em;
        font-weight: 100;
        position: absolute;
        left: 104px; top: -25px;
        text-align: center;
    }
    #paBent {
        position: relative;
    }
    #clock3 {
        font-family: "funny-font";
        font-weight: 100;
        position: relative;
        text-align: center;
        animation: ranibow 1s infinite;
        height: 140px;
    }
    svg {
        width: 100%;
        height: 100%;
        position: relative;
        text-align: center;
    }
    .clock-face {
        fill: rgb(0, 0, 0);
        stroke: rgb(230, 208, 150);
        stroke-width: 1;
        align-items: center;
    }
    .hour {
        stroke: rgb(155, 255, 217);
        stroke-width: 0.8;
        stroke-linecap: round;
    }
    .minuteHand{
        stroke: rgb(155, 255, 217);
        stroke-width: 1.3;
        stroke-linecap: round;
    }
    .hourHand{
        stroke: rgb(155, 255, 217);
        stroke-width: 1.5;
        stroke-linecap: round;
    }
    .firstclock{
        width: 475px;
        height: 321px;
        grid-column: 1;
        grid-row: 1;
    }
    .secondclock{
        max-width: 475px;
        min-width: 150px;
        grid-column: 2;
        grid-row: 1;
        align-items: center;
        text-align: center;
        margin: auto;
    }
    .thirdclock{
        width: 475px;
        height: 321px;
        grid-column: 3;
        grid-row: 1;
    }
    #larm{
        grid-column: 2;
        grid-row: 2;
    }
    .laarmInput{
        text-align: center;
        align-self: center;
        background-color: rgb(0, 0, 0);
        border-color: rgb(0, 0, 0);
        color: rgb(155, 255, 217);
        font-family: Georgia, 'Times New Roman', Times, serif;
    }
    .wkae{
        text-align: center;
        font-size: 50px;
        animation: wakeUps 0.1s infinite;
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        height: 300px;
    }
    .shake {
        height: 500px;
        display: flex;
        place-content: center;
    }
    @media (max-width: 950px){
        main{
            text-align: center;
            align-self: center;
            zoom: 75%;
        }
        .gridthing{
            display: flex;
            flex-direction: column;
        }
        .secondclock{
            width: 230px;
            align-self: auto;
            margin: auto;
        }
        .thirdclock{
            text-align: center;
            margin: auto;
        }
        .laarmInput{
            align-self: center;
            margin: auto;
        }
        
    }
</style>

