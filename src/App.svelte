<script>
  import Character from './components/Character.svelte';
  import svelteIcon from './assets/svelte.svg';

  let page = 1;
  let characters = [];
  let pages = 1;

  async function getCharacters(page = 1) {
    // const response = await fetch('./characters.json');
    const response = await fetch(
      'https://rickandmortyapi.com/api/character?page=' + page,
    );

    const {
      results,
      info: { pages },
    } = await response.json();

    return { characters: results, pages };
  }

  $: getCharacters(page).then((data) => {
    characters = data.characters;
    pages = data.pages;
  });

  function goToPreviusPage() {
    if (page > 1) --page;
  }

  function goToNextPage() {
    if (page <= pages) ++page;
  }
</script>

<h1>
  Rick and Morty
  <img src={svelteIcon} alt="Svelte" style:width="1em" />
</h1>

<div>
  <button on:click={goToPreviusPage} disabled={page <= 1}>Previous</button>
  <button on:click={goToNextPage} disabled={page >= pages}>Next</button>
</div>

<main>
  {#each characters as { id, name, image } (id)}
    <Character {name} {image} />
  {/each}
</main>

<style>
  h1 {
    font-size: 2.7rem;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: .5rem;
    font-family: 'Times New Roman';
    text-align: center;
  }

  :global(body) {
    width: min(90vw, 1200px);
    margin: auto;
    overflow-y: scroll;
  }

  main {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1em;
  }

  div {
    display: flex;
    justify-content: space-between;
    margin-bottom: 1em;
  }

  button {
    padding: 5px 10px;
    border: thin solid white;
    border-radius: 3px;
    background: wheat;
    font-weight: bold;
    color-scheme: light;
  }
</style>
