<script>
  export let image = ''
  export let name = ''
</script>

<article>
  <img src={image} alt={name} width="100%" />
  <h2>{name}</h2>
</article>

<style>
  article {
    background: #101010;
    text-align: center;
    border-radius: 5px;
    overflow: hidden;
  }

  img {
    aspect-ratio: 1 / 1;
    object-fit: cover;
  }
</style>
