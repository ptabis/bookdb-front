<script>
  import BookInfo from "./svelte/BookInfo.svelte";
  import Search from "./svelte/Search.svelte";
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
</style>

<div class="App">
    <BookInfo />
    <Search />
</div>
