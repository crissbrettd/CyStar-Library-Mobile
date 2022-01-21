<script>
  import { createEventDispatcher } from 'svelte';
  import Book from './Book.svelte';
  
  async function loadBookList() {
    const list = await fetch('BookList.json').then(res => res.json());
    console.log(list)
    return list.books
  }

  function handleClickBook(event) {
    console.log(`Clicked book ${event.Book.name}`)
  }

  $: bookList = loadBookList()
</script>   

<div id="mainListDiv">
  {#await bookList}
	  <p>Loading...</p>
  {:then book}
    {#each book as book}
        <Book {...book} on:click={handleClickBook}/>
    {/each}
  {/await}
</div>

<style>

  #mainListDiv {
    padding: 10px;
  }
  /* #exitButtton :active {
    background-color: gray;
  } */

</style>
