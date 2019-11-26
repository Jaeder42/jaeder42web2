<script>
  import Router from "svelte-spa-router";
  import Home from "./views/home.svelte";
  import NotFound from "./views/notFound.svelte";
  import DevLog from "./views/devLog.svelte";
  import Portfolio from "./views/portfolio.svelte";
  import Post from "./views/post.svelte";
  import StateTrak from "./views/statetrak.svelte";
  const routes = {
    "/": Home,
    "/devlog": DevLog,
    "/portfolio": Portfolio,
    "/statetrak": StateTrak,
    "/post/:id": Post,
    "*": NotFound
  };
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    min-height: calc(100vh - 40px);
    display: flex;
    flex: 1;
    flex-direction: column;
    height: 100%;
  }

  content {
    display: flex;
    flex-direction: column;
    flex: 1;
    align-items: center;
  }

  h1 {
    color: whitesmoke;
    text-transform: uppercase;

    font-weight: 100;
    margin: 0;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
    h1 {
      font-size: 4em;
    }
  }
  a {
    margin: 0 15px;
  }

  footer {
    bottom: 5px;
    right: 5px;
  }
</style>

<main>

  <h1>Jæder42</h1>
  <nav>
    <a href="/">Home</a>
    <a href="#/devlog">DevLog</a>
    <a href="#/portfolio">Stuff</a>
  </nav>

  <content>
    <Router {routes} />
  </content>
  <footer>© Johan Jäderblom Krosby, 2019</footer>
</main>
