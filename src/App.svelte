<script>
  import ContactCard from "./components/ContactCard.svelte";
  import FormInvalidation from "./components/FormInvalidation.svelte";
  

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
  let formState = "empty";
  let createdContacts = [];

const addInfoCard = () =>{
  if(
    name.trim().length == 0 ||
    title.trim().length == 0 ||
    image.trim().length == 0 ||
    description.trim().length == 0
  ){
      formState = "invalid"
      return;
  }
// with this, you can't edit values in realtime.
  createdContacts = ([ 
 ... createdContacts,
  { id: Math.random(),
    name:name,
    title:title,
    imageUrl: image,
    desc: description
  }]);

    formState = "done"

}

const deleteFirst = () =>{
  createdContacts= createdContacts.slice(1);
}
const deleteLast = () =>{
  createdContacts = createdContacts.slice(0, -1);
}
</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<button on:click="{addInfoCard}"> Add Contact Info</button>
<button on:click="{deleteFirst}"> Delete first</button>
<button on:click="{deleteLast}"> Delete last</button>



{#if formState === "invalid" }
<FormInvalidation />
{:else}
<p>Please enter some data to complete the form</p>
{/if}

{#each createdContacts as contact, i (contact.id)}
<h1>{ i + 1}</h1>
<ContactCard userName={contact.name} 
jobTitle={contact.jobtitle} 
description={contact.desc} 
userImage={contact.userImage} />
{:else}
<p>Please start adding some data we found none</p>
{/each}
