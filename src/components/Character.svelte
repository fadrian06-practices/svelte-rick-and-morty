<script>
  export let image
  export let name
  export let species
</script>

<article>
  <img src={image} alt={name} />
  <h2>{name}</h2>
  <h3>{species}</h3>
</article>

<style>
  article {
    --radius: 5px;

    background: #101010;
    text-align: center;
    border-radius: var(--radius);
  }

  img {
    border-radius: var(--radius) var(--radius) 0 0;
  }
</style>