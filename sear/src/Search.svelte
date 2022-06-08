<script>
    import { promise } from "./stores.js";
    let question;
    async function search() {
        const res = await fetch(
            `https://demo.dataverse.org/api/search?q=` + question
        );
        const json = await res.json();
         if (res.ok) {
             console.log(json)
            return json;
        } else {
            throw new Error(json);
        } 
    }
</script>

<div>
    <form
        on:submit|preventDefault={() => {
            $promise = search();
        }}
    >
        <input id="searchBar" autocomplete="off" bind:value={question} />
    </form>
</div>

<style>
    div {
        display: flex;
        gap: 10px;
        width: 50%;
        justify-self: center;
        align-items: center;     
    }
    form,
    form input {
        width: 100%;
    }
    #searchBar {
        background-color: aliceblue;
        border-color: transparent;
    }
    #searchBar:focus {
        outline: none;
    }
    @media (max-width: 700px) {
        div {
            width: 90%;
        }
    }
</style>