<script>
  import Book from './Book.svelte';
  import BookList from './BookList.svelte';
  import Form from './EditBook.svelte';
  import Popout from './Popout.svelte';
  
  let shouldShowBookList = false;

  function showBookList() {
    shouldShowBookList = !shouldShowBookList;
  }

  // function handleItemAdd(event) {
  //     itemList = [...itemList, { 
  //     id: itemList.length,
  //     location: event.detail.location,
  //     total: event.detail.total,
  //     category: event.detail.category
  //     }]
  //     shouldShowForm = event.detail.showForm;
  // }

  function handleCloseList()  {
    showBookList()
  }

  // function handleBookClick(event) {
  //     console.log(itemList);
  //     itemList = itemList
  //         .filter((element) => {return element.detail.id !== event.detail.id})
  // }

  // function handleRemovePurchase(event) {
  //     console.log(itemList);
  //     itemList = itemList
  //         .filter((element) => {return element.detail.id !== event.detail.id})
  // }

  function savePurchaseList() {
      const json = JSON.stringify(itemList, null, 4);
      localStorage.setItem("purchase-list", json);
      console.log("saved")
  }

  function clearPurchaseList() {
      localStorage.setItem("purchase-list", []);
      itemList = []
  }


</script>

<main>
    <h1>Library<br/>Companion</h1>
    <div id="mainDiv">        
        <div id="buttonContainer">
            <button class="mainButton" on:click={showBookList}>
                Update a book
            </button>
            <br />
            <button class="mainButton" on:click={savePurchaseList}>
                View book list
            </button>
            <br />
            <button class="mainButton" on:click={clearPurchaseList}>
                Browse wishlist
            </button>
        </div>
    </div>
    
    {#if shouldShowBookList}
        <Popout>
            <BookList on:closeForm={handleCloseList}/>
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