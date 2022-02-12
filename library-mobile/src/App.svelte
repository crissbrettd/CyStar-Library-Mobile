<script>
  import Book from './Book.svelte';
  import BookList from './BookList.svelte';
  import Form from './EditBook.svelte';
  import Popout from './Popout.svelte';
  import WishList from './WishList.svelte';
  let shouldShowFullBookList = false;
  let shouldShowActiveBookList = false;
  let shouldShowWishList = false;

  function closePopout() {
    shouldShowFullBookList = false;
    shouldShowActiveBookList = false;
    shouldShowWishList = false;
  }

  function showActiveBookList() {
    shouldShowActiveBookList = !shouldShowActiveBookList;
  }

  function showFullBookList() {
    shouldShowFullBookList = !shouldShowFullBookList;
  }

  function showWishList() {
    shouldShowWishList = !shouldShowWishList;
  }

  function handleActiveBookSelected(event)  {
    let selectedBook = event.detail;
    console.log(selectedBook);
  }

  function handleOwnedBookSelected(event)  {
    let selectedBook = event.detail;
    console.log(selectedBook);
  }

  function handleWishListBookSelected(event)  {
    let selectedBook = event.detail;
    console.log(selectedBook);
  }

  function handleBookListClosed(event)  {
    closePopout();
  }

  function handleWishListClosed(event)  {
    closePopout();
  }

</script>

<main>
    <h1>Library<br/>Companion</h1>
    <div id="mainDiv">        
        <div id="buttonContainer">
            <button class="mainButton" on:click={showActiveBookList}>
                Update a book
            </button>
            <br />
            <button class="mainButton" on:click={showFullBookList}>
                View full book list
            </button>
            <br />
            <button class="mainButton" on:click={showWishList}>
                Browse wishlist
            </button>
        </div>
    </div>
  
    {#if shouldShowFullBookList}
      <Popout>
          <BookList activeOnly={false} on:bookSelected={handleActiveBookSelected} on:listClosed={handleBookListClosed} />
      </Popout>
    {/if}
    {#if shouldShowActiveBookList}
      <Popout>
          <BookList activeOnly={true} on:bookSelected={handleOwnedBookSelected} on:listClosed={handleBookListClosed} />
      </Popout>
    {/if}
    {#if shouldShowWishList}
      <Popout>
          <WishList on:bookSelected={handleWishListBookSelected} on:listClosed={handleWishListClosed} />
      </Popout>
    {/if}
</main>



<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 500px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

    .mainButton {
        color: #ff3e00;
        margin-top: 10px;
    }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>