<script>
  import Character from './components/Character.svelte'
  // import mock from './mock.json'
  // const apiPromise = Promise.resolve(mock)
  let page = 1;
  $: apiPromise = fetch(
    `https://rickandmortyapi.com/api/character?page=${page}`,
  ).then((response) => response.json());

  function moveToNextPage() {
    page += 1
  }

  function moveToPreviousPage() {
    if (page > 1) {
      page -= 1
    }
  }
</script>

<h1>Rick and Morty Svelte</h1>
<main>
  <header>
    <button disabled={page === 1} on:click={moveToPreviousPage}>
      Previous
    </button>
    <button on:click={moveToNextPage}>Next</button>
  </header>
  {#await apiPromise}
    <p>Loading...</p>
  {:then apiBody}
    <ul>
      {#each apiBody.results as character (character.id)}
        <li>
          <Character {...character} />
        </li>
      {/each}
    </ul>
  {/await}
</main>

<style>
  h1 {
    font-size: 2.7rem;
    font-weight: bolder;
    text-align: center;
  }

  main {
    max-width: 1200px;
    margin: auto;
  }

  ul {
    list-style: none;
    padding: 0;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1rem;
  }

  li {
    list-style: none;
  }

  header {
    display: flex;
    justify-content: space-between;
    padding-bottom: 2px;
  }

  button {
    padding: 5px 10px;
    border: 1px solid white;
    border-radius: 3px;
    background: wheat;
    font-weight: bold;
  }
</style>