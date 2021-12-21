<script>
    export let country
    export let description
    export let image 
    export let visitAgain 
    export let _id
    export let action
    export let create
    export let update



    //functions
    const handleSubmit = (event) => {
        event.preventDefault()
        if(action === "create"){
            create({country, description, image, visitAgain})
        }
        if(action === "update"){
            update({country, description, image, _id, visitAgain})
        }
    }

</script>

<div>
    <form on:submit={handleSubmit}>
        Location:
        <input type="text" bind:value={country}>
        Description:
        <input type="text" bind:value={description}>
        Image Url:
        <input type="text" bind:value={image}>
        Visit Again?
        <input type="checkbox" bind:checked={visitAgain}>
        <input type="submit">
    </form>
    
</div>