<script>
  import {onMount} from "svelte"
  import Display from "./components/Display.svelte"
  import Form from "./components/Form.svelte"
  import Modal from "./components/Modal.svelte"

  const url = "https://travellog-backend-ll.onrender.com"

  // state
  let showForm = false 
  let country = ""
  let description = ""
  let image = ""
  let visitAgain = false
  let _id = ""
  let travellogs = []
  let action = "create"
  let modal;

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
  <h1 class="title">
    trav<span>log</span>
  </h1>
  
  <div class="button">
    <button class="modal-question" on:click={() => modal.show()}>?</button>
      <Modal bind:this={modal}>
        <div class="modal-text">
          <h2>Welcome to Travlog</h2>
          <p>Never forget your favourite travel memories! You can write down your favourite spots and decide if you want to revisit.</p>
        </div>
        <button class="close" on:click={() => modal.hide()}></button>
      </Modal>
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

*{
  font-family: 'Roboto', sans-serif;
}

span {
color: #97BFB4;
font-family: 'Dosis', sans-serif;
}

.title {
  font-family: 'Dosis', sans-serif;
  font-size: 5em;
  text-align: center;
  margin-top: 1%;
}

.button {
  text-align: right;
  margin-right: 6em;
}

@media screen and (max-width: 500px) {
  .button {
    width: 95%;
    margin-right: 3em;
  }
}


.new-log {
  box-shadow: 5px 5px 5px #888888;
  padding:0.35em 1.2em;
  border:0.1em solid #FFFFFF;
  margin:0 0.3em 0.3em 0;
  border-radius:0.12em;
  font-family:'Roboto',sans-serif;
  font-weight:300;
  color: black;
  transition: all 0.2s;
}

.new-log:hover{
  color:#000000;
  background-color:#97BFB4;
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

.modal-question:hover {
  background-color: #97BFB4;
  border: lightgrey;

}

.modal-question {
  box-shadow: 5px 5px 5px #888888;
  padding:0.35em .8em;
  border:0.1em solid #FFFFFF;
  margin:0 0.3em 0.3em 0;
  border-radius:1em;
  font-family:'Roboto',sans-serif;
  font-weight:300;
  color: black;
  transition: all 0.2s;
}

.modal-text {
  text-align: center;
}

.close {
  border: none;
}


</style>

