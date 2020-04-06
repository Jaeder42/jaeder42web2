<script>
  import axios from "axios";
  import LineChart from "../components/LineChart.svelte";
  let data = null;
  let cases = [];
  let deaths = [];
  const getData = async () => {
    const result = await axios.get(
      "https://jaeder-covid-api.herokuapp.com/list"
    );
    data = result.data;
    deaths = data.results.map(result => ({
      date: result.date,
      value: result.totalDeaths
    }));
    cases = data.results.map(result => ({
      date: result.date,
      value: result.totalCases
    }));
    console.log(cases);
  };
  getData();
</script>

<style>
  main {
    margin: 40px 0px;
    width: 100%;
    height: 100vh;
  }
  h1 {
    font-weight: 100;
  }
  .chart {
    max-height: 500px;
  }
</style>

<main>
  <h1>COVID-19 in Sweden 🇸🇪</h1>
  {#if data}
    <div class="chart">
      <LineChart class="chart" title="" data={cases} dataComp={deaths} />
    </div>
  {/if}
  {#if !data}
    <p>...loading data</p>
  {/if}
</main>
