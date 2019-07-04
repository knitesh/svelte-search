<link rel='stylesheet' href='https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css' type='text/css'
 media='all'>
<script>
  let searchTerm = "";
  let result = [];

  const API_KEY = "eOkQduGgkC8zUHDYmkPklqHu0J1oIvgc";
  const searchUrl =
    "https://api.giphy.com/v1/gifs/search?api_key=" +
    API_KEY +
    "&limit=25&offset=0&rating=G&lang=en&q=";

  const searchFunction = async event => {
    event.preventDefault();
    const response = await fetch(`${searchUrl}${searchTerm}`);
    const json = await response.json();
    result = json.data.map(data => data.images.fixed_width.url);
  };
</script>

<style>
  .gif-image {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin-top: 2em;
  }
</style>

<main class="container container-small">
	<h1 class="text-center">Svelte Search</h1>
	<form on:submit={searchFunction} class="form">
    <div class="form-group">
      <label for="searchTerm">Enter Search Term</label>
      <input id="searchTerm" class="form-control" type="text" bind:value={searchTerm}>
    </div>
    <button type="submit" class="btn btn-primary">Search</button>
  </form>
  <div class="gif-image row">
    {#if result.length }
      {#each result as src}
      <img alt="gif-giphy" {src}> 
      {/each}
    {:else}
      <span>Enter new search term</span> 
    {/if}
  </div>
</main>