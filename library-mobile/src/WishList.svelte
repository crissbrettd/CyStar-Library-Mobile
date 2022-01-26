<script>
  import { createEventDispatcher } from 'svelte';
  import Book from './Book.svelte';

  const dispatch = createEventDispatcher();
  
  async function loadBookList() {
    const list = await fetch('BookList.json').then(res => res.json());
    return list.books
  }

  function handleClickBook(event) {
    dispatch('bookSelected', event.detail)
  }

  function handleCloseButton() {
    console.log("closed list")
    dispatch('listClosed')
  }

  $: bookList = loadBookList()
</script>   

<div id="mainListDiv">
  {#await bookList}
	  <p>Loading...</p>
  {:then book}
    {#each book as book}
      {#if book.isStarted == true && book.isCompleted == false}
        <Book {...book} on:clickBook={handleClickBook}/>
      {/if}
    {/each}
  {/await}
  <div id="closeButton" on:click={handleCloseButton}>
    <p>Close</p>
  </div>
</div>

<style>

  #mainListDiv {
    padding: 10px;
  }
  
  #closeButton {
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
    width: 50%;
    z-index: 0;
  }
</style>
