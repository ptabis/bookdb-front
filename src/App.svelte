<script>
  import Quagga from "./svelte/Quagga.svelte";
  import SearchButton from "./svelte/SearchButton.svelte";
</script>

<style>
  /*
  #224957
  #A3DDF0
  #54B6D6
  #4E585C
  #408AA3
  */
  :global(body) {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
    position: relative;
    background-color: #224957;
  }
  .App {
    text-align: center;
  }
  .SearchButton {
    position: fixed;
    bottom: 10px;
    right: 10px;
  }
</style>

<div class="App">
    <p>
      <Quagga />
    </p>
    <div class="SearchButton">
      <SearchButton />
    </div>
</div>
