<script>
  import { createEventDispatcher } from 'svelte';
  export let name;
  export let isbn;
  export let authorFirstName;
  export let authorLastName;
  export let length;
  export let genre;
  export let description;
  export let isStarted;
  export let isCompleted;
  export let currentPage;

  const dispatch = createEventDispatcher();

  function editBook() {
    dispatch('clickBook', {
      name: name,
      isbn: isbn,
      authorFirstName: authorFirstName,
      authorLastName: authorLastName,
      length: length,
      genre: genre,
      description: description,
      isStarted: isStarted,
      isCompleted: isCompleted,
      currentPage: currentPage
      })
  }
</script>

<div on:click={editBook}>
  <p>{name}</p>
</div>

<style>
  div {
    background-color: #ff3e00;
    border-color: white;
    border-radius: 10px;
    border-style: solid;
    border-width: 1px;
    color: white;
    margin: auto;
    margin-bottom: 5px;
    margin-top: 5px;
    user-select: none;
    width: 90%;
    z-index: 0;
  }
</style>