<script>
  import { Router, Link, Route } from "svelte-routing";
  import Home from "./screens/Home.svelte";
  import Details from "./screens/Details.svelte";
  import Navbar from "./components/Navbar.svelte";
  import { links } from "svelte-routing";

  export let url = "";
</script>

<Router {url}>
  <Navbar />
  <div>
    <Route path="/">
      <Home />
    </Route>
    <Route path="details/:id" component={Details} />
  </div>
</Router>
