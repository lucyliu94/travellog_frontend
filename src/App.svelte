<script>
  import {onMount} from "svelte"
  import Display from "./components/Display.svelte"
  import Form from "./components/Form.svelte"
  import Modal from 'svelte-simple-modal';

  const url = "https://travellogbackend-ll.herokuapp.com/travellogs"

  // state
  let showForm = false 
  let country = ""
  let description = ""
  let image = ""
  let visitAgain = false
  let _id = ""
  let travellogs = []
  let action = "create"

  //functions
  const getTravellogs = async () => {
    const response = await fetch(url)
    const data = await response.json()
    travellogs = data
  }

  //show form
  const toggleForm = () => {
    showForm = !showForm
  }

  const resetState = () => {
    country = ""
    description = ""
    image = ""
    visitAgain = false
    showForm = false
    _id = ""
    action="create"
    getTravellogs()
  }

  //create todo
  const createTravellogs = async (travellog) => {
    await fetch(url, {
      method: "post",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(travellog)
    })
    resetState()
  }

const selectTravellogToUpdate = (travellog) => {
  country = travellog.country
  description = travellog.description
  image = travellog.image 
  visitAgain = travellog.visitAgain
  _id = travellog._id
  action = "update"
  showForm = true
}

const updateTravellogs  = async (travellog) => {
    await fetch(url +`/${travellog._id}`, {
      method: "put",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(travellog)
    })
    resetState()
  } 

const deleteTravellogs  = async (travellog) => {
    await fetch(url +`/${travellog._id}`, {
      method: "delete",
    })
    resetState()
  } 


//Life cycle
onMount(() => { getTravellogs() })

</script>

<main>
  <h1 class="title">travlog</h1>
  <div class="button">
    <button class="new-log bouncy" on:click={toggleForm}>Create New Log</button>
  </div>
  {#if showForm}
  <Form
    country={country}
    description={description}
    image={image}
    visitAgain={visitAgain}
    _id={_id}
    action={action}
    create={createTravellogs}
    update={updateTravellogs}
  />
  {/if}
  <Display 
    travellogs={travellogs} 
    select={selectTravellogToUpdate}
    destroy={deleteTravellogs}
  />

</main>

<style>


.title {
  font-family: 'Dosis', sans-serif;
  font-size: 5em;
  text-align: center;
  margin-top: 1%;
}

.button {
  text-align: right;
  margin-right: 5%;
}

.new-log {
  padding:0.35em 1.2em;
  border:0.1em solid #FFFFFF;
  margin:0 0.3em 0.3em 0;
  border-radius:0.12em;
  box-sizing: border-box;
  text-decoration:none;
  font-family:'Roboto',sans-serif;
  font-weight:300;
  color: black;
  transition: all 0.2s;
}

.new-log:hover{
  color:#000000;
  background-color:#FFFFFF;
}

.bouncy{
  animation: bouncy 5s infinite linear;
  position:relative;
}

@keyframes bouncy {
  0%{top:0em}
  40%{top:0em}
  43%{top:-0.9em}
  46%{top:0em}
  48%{top:-0.4em}
  50%{top:0em}
  100%{top:0em;}
}
</style>

