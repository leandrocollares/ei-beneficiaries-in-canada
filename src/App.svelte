<script>
  import * as d3 from 'd3';
  import Header from './components/Header.svelte';
  import LineChart from './components/LineChart.svelte';
  import Footer from './components/Footer.svelte';
  import Select from 'svelte-select';
  import { geographies } from '../public/data/geographies.js';

  let beneficiaryData;

  $: value = geographies[0];

  d3.csv('../data/beneficiaries.csv').then(data => (beneficiaryData = data));

  const handleSelect = event => {
    value = event.detail.value;
  };

  const handleClear = () => {
    value = null;
  };
</script>

<main>
  <div class="app">
    <Header geography={value} />
    <div class="selector">
      <Select
        items={geographies}
        {value}
        placeholder="Select geography..."
        inputStyles="font-family: Lato;"
        on:select={handleSelect}
        on:clear={handleClear}
      />
    </div>

    {#if beneficiaryData && value}
      <LineChart data={beneficiaryData.filter(d => d.geography === value)} />
    {/if}
    <Footer />
  </div>
</main>

<style>
  @font-face {
    font-family: 'Merriweather';
    font-style: normal;
    font-weight: 700;
    src: local(''),
      url('../fonts/merriweather-v25-latin-700.woff2') format('woff2'),
      url('../fonts/merriweather-v25-latin-700.woff') format('woff');
  }

  @font-face {
    font-family: 'Lato';
    font-style: normal;
    font-weight: 400;
    src: local(''), url('../fonts/lato-v20-latin-regular.woff2') format('woff2'),
      url('../fonts/lato-v20-latin-regular.woff') format('woff');
  }

  @font-face {
    font-family: 'Lato';
    font-style: normal;
    font-weight: 700;
    src: local(''), url('../fonts/lato-v20-latin-700.woff2') format('woff2'),
      url('../fonts/lato-v20-latin-700.woff') format('woff');
  }

  :root {
    font-family: 'Lato', sans-serif;
    font-size: 16px;
    color: #282828;
    background: #ffffff;
    margin: 0 15px;
  }

  .app {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    width: 100%;
    user-select: none;
  }

  .selector {
    width: 260px;
    margin-bottom: 10px;
    --border: 1px solid #bdc3c7;
    --borderFocusColor: #4427ca;
    --borderHoverColor: #4427ca;
    --borderRadius: 2px;
    --clearSelectColor: #bdc3c7;
    --clearSelectFocusColor: #4427ca;
    --clearSelectHoverColor: #4427ca;
    --inputColor: #282828;
    --inputFontSize: 16px;
    --itemColor: #282828;
    --itemIsActiveColor: #ffffff;
    --itemIsActiveBG: #4427ca;
    --itemHoverBG: rgb(68, 39, 202, 0.2);
    --listBorderRadius: 2px;
    --placeholderColor: #282828;
  }
</style>
