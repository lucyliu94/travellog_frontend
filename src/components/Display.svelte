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
            <h4>Visit Again? --> {travellog.visitAgain}</h4>
            <button on:click={() => destroy(travellog)}>Delete</button>
        </div>

        {/each}
    
</div>

<style>
    .container {
        display: flex;
        flex-wrap: wrap;
    }
    .card {
        width: 20%;
        margin: 5% auto;
        border: 1px solid lightgrey;
        padding: 2% 10%;
    }

    img {
        width: 100%;
    }
</style>