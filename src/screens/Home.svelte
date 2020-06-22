<script>
  import { onMount } from "svelte";
  import { navigate } from "svelte-routing";

  const apiKEY = "1159c700087c4037b4bd335031f56c6e";
  const dataUrl = `https://newsapi.org/v2/everything?q=javascript&sortBy=publishedAt&apiKey=${apiKEY}`;
  let items = [];
  let id = "";
  let src = "placeholder.png";
  const fetchData = async () => {
    const response = await fetch(dataUrl);
    const data = await response.json();
    items = data["articles"];
  };
  const getUniqueData = async title => {
    const response = await fetch(dataUrl);
    const data = await response.json();
    const id = data["articles"].findIndex(item => item.title === title);
    navigate(`details/${id}`);
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
    border-radius: 3px;
    text-align: center;
    background: #fff;
    border-radius: 2px;
    display: inline-block;
    margin: 0.2rem;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
    transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
  }
  .card:hover {
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
  }
  a {
    color: #333;
    font-weight: 600;
    font-size: 1.3em;
  }
  main {
    background: #ecf0f1;
  }
  .desc {
    word-break: break-all;
    word-break: break-all;
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
          <p class="desc">{item.description}</p>
          <a on:click={getUniqueData(item.title)}>Détails</a>
        </div>
      </div>
    {/each}

  </div>
</main>
