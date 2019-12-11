<script>
  let feed = [
    "searching for squirrels",
    "downloading history",
    "fetching bitcoins"
  ];
  let texts = ["hacking in progress"];
  let index = 0;
  let points = 1;
  let pointText = ".";
  let done = false;

  const step = () => {
    texts[index] = texts[index] + " DONE";
    texts.push(feed.pop());
    texts.push();
    index++;
    if (feed.length > 0) {
      setTimeout(step, 4000);
    } else {
      setTimeout(() => {
        texts[index] = texts[index] + " DONE";
        texts.push("just kidding :)");
        texts.push("check out the devLog!");
        done = true;
      }, 4000);
    }
  };

  setInterval(() => {
    if (points < 3) {
      points += 1;
    } else {
      points = 1;
    }
    pointText = ".".repeat(points);
  }, 300);
  setTimeout(step, 4000);
</script>

<style>
  screen {
    background-color: #aaa;
    padding: 30px 10px;
    display: flex;
    flex-direction: column;
    position: relative;
    border-radius: 5px;
  }
  console {
    background: black;
    min-height: 300px;
    height: 100%;
    display: flex;
    border-radius: 20px;
    padding: 10px;
    flex-direction: column;
    color: greenyellow;
    justify-content: flex-end;
    align-items: flex-start;
    white-space: nowrap;
    overflow: hidden;
  }
  main {
    width: 100%;
    max-width: 400px;
    padding-top: 20px;
    position: relative;
  }

  lines {
    font-family: "Press Start 2P";
    font-size: 10px;
    display: flex;
    justify-content: flex-start;
    flex-direction: row;
    text-align: left;
    margin-top: 14px;
  }
</style>

<main>
  <screen>
    <console>
      {#each texts as text, i}
        <lines>
          $ > {text}
          {#if i == index && !done}{pointText}{/if}
        </lines>
      {/each}
    </console>
    <h2>HACKINTOSH 2.0</h2>
  </screen>
</main>
