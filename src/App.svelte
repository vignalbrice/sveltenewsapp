<script>
  import { onMount } from "svelte";

  const apiKEY = "1159c700087c4037b4bd335031f56c6e";
  const dataUrl = `https://newsapi.org/v2/everything?q=javascript&sortBy=publishedAt&apiKey=${apiKEY}`;
  let items = [];
  let src = "placeholder.png";
  const fetchData = async () => {
    const response = await fetch(dataUrl);
    const data = await response.json();
    console.log(data["articles"]);
    items = data["articles"];
  };

  onMount(() => fetchData());
</script>

<style>
  h1 {
    color: #333;
    font-family: "Comic Sans MS";
    text-align: center;
    font-weight: 600;
  }
  .container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(305px, 1fr));
    grid-gap: 15px;
  }
  .container > .card img {
    max-width: 100%;
  }
  .card {
    padding: 5px;
    border: #333 0.5px solid;
    border-radius: 3px;
    text-align: center;
  }
  a {
    color: #333;
    font-weight: 600;
    font-size: 1.3em;
  }
</style>

<main>
  <h1>Daily News</h1>
  <hr />
  <br />
  <div class="container">
    {#each items as item}
      <div class="card">
        <img
          src={item.urlToImage ? item.urlToImage : src}
          alt={item.urlToImage} />
        <div class="card-body">
          <h3>{item.title}</h3>
          <p>{item.description}</p>
          <a href={item.url}>Read</a>
        </div>
      </div>
    {/each}

  </div>
</main>
