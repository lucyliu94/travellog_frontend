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
        <label>Location 
            <input type="text" placeholder="i.e city, country..." bind:value={country}>
        </label>
        <label>
            Description
            <input type="text" placeholder="beautiful sceneries..." bind:value={description}>
        </label>
        <label>
            Image Url
            <input type="text" bind:value={image}>
        </label>
       <label>
        Visit Again?
        <input class="checkbox" type="checkbox" bind:checked={visitAgain}>
       </label>
        <label class="submitlabel">
            <input class="submit" type="submit">
        </label>
    </form>
    
</div>

<style>

* {
    font-family: 'Roboto', sans-serif;
}
form {
    background: white;
    border: 1px solid #dedede;
    display: flex;
    flex-direction: column;
    margin: 0 auto;
    width: 40%;
    padding: 30px 70px;
    background-color: white;
    box-shadow: 5px 5px 5px lightgrey;
}

input {
   border: 1px solid #d9d9d9;
   padding: 10px;
   width: 100%;
   margin-bottom: 10px;
   margin-top: 10px;
}

label {
    text-align: center;
}

.checkbox {
    background-color: purple;
}

.submitlabel {
    text-align: center;
}
.submit {
    width: 20%;
    text-align: center;
    border-radius: 10px;
}

.submit:hover {
    box-shadow: 2px 2px 2px lightgrey;
    transform: scale(1.05);
}


</style>