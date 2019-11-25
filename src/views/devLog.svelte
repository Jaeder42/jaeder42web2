<script>
  import axios from "axios";
  import dayjs from "dayjs";
  import { push } from "svelte-spa-router";

  let posts = null;
  const getPosts = async () => {
    const result = await axios.get(
      `https://us-central1-project-4786714231348226511.cloudfunctions.net/post/get`
    );
    posts = result.data;
  };

  getPosts();

  const goToPost = id => {
    push(`/post/${id}`);
  };
</script>

<style>
  main {
    margin: 40px 0px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
  }

  post {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin: 20px 20px;
    max-width: 200px;
    border: 1px solid #3a3347;
    min-height: 100px;
    border-radius: 10px;
    padding: 20px;
    -webkit-box-shadow: 0px 0px 3px 0px rgba(0, 0, 0, 0.75);
    -moz-box-shadow: 0px 0px 3px 0px rgba(0, 0, 0, 0.75);
    box-shadow: 0px 0px 3px 0px rgba(0, 0, 0, 0.75);
    background-color: teal;
    cursor: pointer;
    filter: grayscale();
    transition: all 1s;
  }

  post:hover {
    filter: none;
    transform: scale(1.1);
  }

  postTitle {
    font-size: 18px;
  }
  subTitle {
    font-size: 12px;
  }
</style>

<main>
  {#if posts}
    {#each posts as post}
      <post on:click={() => goToPost(post.id)}>
        <postTitle>{post.title}</postTitle>
        <subTitle>{post.subTitle}</subTitle>
        <subTitle>{dayjs(post.date).format('YYYY-MM-DD')}</subTitle>
      </post>
    {/each}
  {/if}
  {#if !posts}...loading{/if}

</main>
