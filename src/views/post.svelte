<script>
  import axios from "axios";
  export let params = {};
  let post = null;
  const getPost = async () => {
    if (params.id === "latest") {
      const result = await axios({
        method: "GET",
        url: `https://us-central1-project-4786714231348226511.cloudfunctions.net/post/latest`
      });
      post = result.data;
    }
    const result = await axios({
      method: "GET",
      url: `https://us-central1-project-4786714231348226511.cloudfunctions.net/post/get-post/${params.id}`
    });
    post = result.data;
    console.log(result.data);
  };

  getPost();
</script>

<style>
  main {
    margin: 40px 0px;
  }
  content {
    display: flex;
    overflow-x: hidden;
  }
</style>

<main>
  <content>
    {#if post}
      <post>
        {@html post.content}
      </post>
    {/if}
  </content>
</main>
