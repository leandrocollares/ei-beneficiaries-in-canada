<script>
  export let geography;
</script>

<header>
  <h1>
    Regular Employment Insurance (EI) beneficiaries in {geography
      ? geography
      : 'Canada'}
    (2019 - 2021)
  </h1>
</header>

<style>
  header {
    margin-top: 25px;
    margin-bottom: 20px;
    max-width: 600px;
  }

  h1 {
    font-family: 'Merriweather';
    font-size: 22px;
    line-height: 30px;
    text-align: center;
  }
</style>
