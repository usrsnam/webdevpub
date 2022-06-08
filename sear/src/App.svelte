<script>
    import Spinner from "./Spinner.svelte";
    import Results from "./Results.svelte";
    import Search from "./Search.svelte";
    import { promise } from "./stores.js";
    let darkmode = false;
    function handleClick() {
        darkmode =! darkmode
    }
</script>

<main class:darkmode class:search={$promise != undefined}>
    <button class:darkmode class="buton" on:click ={handleClick}>
        DORK MODE
    </button>
    <p class="siteName">
        <span style='color: #69E3BC'>G</span>
        <span style='color: #DF5A98'>o</span>
        <span style='color: #EAD759 '>o</span>
        <span style='color: #69E3BC'>b</span>
        <span style='color: #8BC275'>l</span>
        <span style='color: #DF5A98 '>e</span>
    </p>

	<Search/>
	{#await $promise}
		<Spinner />
	{:then result}
		<Results json={result} />
	{:catch error}
		<p style="color: red">{error.message}</p>
	{/await}
</main>

<style>
    :global(body) {
        padding: 0;
        margin: 0;
		overflow: hidden;
        overflow: hidden;
		height: 100%;
		width: 100%;
		z-index: -1;
		position: fixed;
    }
    .siteName {
        -webkit-text-stroke: transparent;
        font-size: 150px;
        margin-bottom: 0px;
        margin-top: 0px;
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        letter-spacing: -0.05em;
    }
    main {
        height: 100vh;
        width: 100vw;
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        gap: 40px;
        padding-top: 10%;
        padding-left: 10%;
        padding-right: 10%;
        padding-bottom: 5%;
        box-sizing: border-box;
        background: conic-gradient( rgb(222, 215, 200) 65deg, rgb(200, 183, 154) 65deg, rgb(200, 183, 154) 115deg, rgb(231, 228, 222) 115deg, rgb(231, 228, 222) 295deg, rgb(222, 215, 200) 295deg);
        transition: all 0.05s;
    }
    main.search {
        padding-top: 0%;
        gap: 5px;
    }
    main.darkmode {
        background: conic-gradient( rgb(93, 93, 93) 65deg, rgb(75, 75, 75) 65deg, rgb(75, 75, 75) 115deg, rgb(110, 110, 110) 115deg, rgb(110, 110, 110) 295deg, rgb(93, 93, 93) 295deg);
    }
    .buton {
        background: transparent;
        border-color: rgb(200, 183, 154);
        border-width: 4px;
        border-radius: 4px;
        width: 58px;
        height: 58px;
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        color: rgb(200, 183, 154);
        position: absolute;
        left: 10px;
        top: 10px;
    }
    .buton.darkmode {
        border-color: rgb(75, 75, 75);
        color: rgb(75, 75, 75);
    }
    @media (max-width: 700px) {
        main {
            background: conic-gradient(rgb(200, 183, 154) 45deg, rgb(222, 215, 200) 45deg, rgb(222, 215, 200) 135deg, rgb(231, 228, 222) 135deg, rgb(231, 228, 222) 315deg, rgb(200, 183, 154) 315deg);
            gap: 38px;
        }
        .siteName {
            font-size: 400%;
            -webkit-text-stroke: transparent;
        }
        main.search {
            margin-top: auto;
            gap: 40px;
        }
        main.darkmode {
            background: conic-gradient( rgb(75, 75, 75) 45deg, rgb(93, 93, 93) 45deg, rgb(93, 93, 93) 135deg, rgb(110, 110, 110) 135deg, rgb(110, 110, 110) 315deg, rgb(75, 75, 75) 315deg);
        }
        .buton {
            position: absolute;
            color: rgb(231, 228, 222);
            border-color: rgb(231, 228, 222);
        }
        .buton.darkmode {
            color: rgb(110, 110, 110);
            border-color: rgb(110, 110, 110);
        }
    }
</style>