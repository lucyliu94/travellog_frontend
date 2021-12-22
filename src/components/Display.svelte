<script>
    export let travellogs;
    export let select;
    export let destroy;
</script>

<div class="container">
        {#each travellogs as travellog}
        <div class="card">
            <img src="{travellog.image}" alt="">
            <h1 class="countryName" on:click={() => select(travellog)}>{travellog.country}</h1>
            <h3>{travellog.description}
            </h3>
            <h4>Visit Again: {travellog.visitAgain}</h4>
            <button class="trash" on:click={() => destroy(travellog)}>🗑️</button>
        </div>

        {/each}
    
</div>

<style>
    .container {
        display: flex;
        flex-wrap: wrap;
    }
    .card {
        width: 25%;
        margin: 5% auto;
        border: 1px solid lightgrey;
        padding: 2% 5%;
        box-shadow: 5px 10px 18px #888888;
        border-radius: 2%;
    }

    @media screen and (max-width: 375px) {
        .card {
            width: 85%;
            height: 100%;
        }
}

    .card:hover{
        border: 1px solid lightgrey;
        box-shadow: 5px 10px 18px black;
        cursor:pointer;
    }

    img {
        width: 100%;
        height: 30%;
    }

    .trash {
        border: none;
        background: white;
    }

    .trash:hover{
        cursor: pointer;
        transform:scale(1.5);
    }
</style>

