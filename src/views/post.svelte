<script>
  import axios from "axios";
  import dayjs from "dayjs";
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
    text-align: left;
    max-width: 600px;
  }
  post {
    display: flex;
    flex-direction: column;
  }
  postTitle {
    font-size: 20px;
    font-weight: bold;
  }
  subtitle {
    font-size: 14px;
    margin-bottom: 20px;
    margin-right: 6px;
  }
  row {
    display: flex;
  }
</style>

<main>
  <content>
    {#if post}
      <post>
        <postTitle>{post.title}</postTitle>
        <row>
          <subtitle>{post.subTitle}{', '}</subtitle>
          <subtitle>{dayjs(post.date).format('YYYY-MM-DD')}</subtitle>
        </row>
        {@html post.content}
      </post>
    {/if}
    {#if !post}
      <h2>Loading...</h2>
    {/if}
  </content>
</main>
