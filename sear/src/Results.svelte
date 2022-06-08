<script>
    export let json;
    import { fly, fade, slide, draw } from "svelte/transition";
</script>

{#if json && "data" in json && "items" in json.data && json.data.items.length > 0}
    <div id = "item-holder">
        {#each json.data.items as item}
            <div id = "item">
                <h1 id="title">{item.name}</h1>
                <p>{item.type}</p>
                <p>{item.url}</p>
                <p>{item.identifier}</p>
                <p>{item.description}</p>
                <p>{(item.published_at).substr(0, 10)}</p>
            </div>
        {/each}
    </div>
{:else if json}
    <div class="funnyInput">
        <p in:fade>You got fucked.</p>
    </div>
{/if}

<style>
    #item-holder {
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        overflow-y: scroll;
        box-sizing: border-box;
        padding-left: 10%;
        padding-right: 10%;
        max-width: 100%;
        row-gap: 15px;
    }
    #item {
        border-radius: 3px;
        background-color: aliceblue;
        border: transparent;
        padding: 20px;
        width: 100%;
        box-sizing: border-box;
        word-wrap: break-word;
    }
    .funnyInput {
        font-size: 30px;
        color: aliceblue;
        -webkit-text-stroke: 2px black;
        font-family: Georgia, 'Times New Roman', Times, serif;
        font-style: italic;
    }
    p {
        border: transparent;
        padding: 5px;

    }
    ::-webkit-scrollbar {
        width: 9px;
        height: 15px;

    }
    ::-webkit-scrollbar-track {
        border-radius: 3px;
        background-color: rgba(0, 0, 0, 0.1);
    }
    ::-webkit-scrollbar-thumb {
        background-color:  rgba(209, 226, 224, 0.8);
        border-radius: 3px;
        height: 100px;
    }
    @media (max-width: 700px) {
        #item {
        font-size: 20px;
    }
    #title {
        font-size: 20px;
    }
    #item-holder {
        padding: 0%;
    }
    }
</style>