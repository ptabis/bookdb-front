<script>
    import Quagga from "./Quagga.svelte";
    import SearchButton from "./SearchButton.svelte";
</script>

<style>

    .SearchButton {
        position: fixed;
        bottom: 10px;
        right: 10px;
    }
</style>

<div>
    <div>
      <Quagga />
    </div>
    <div class="SearchButton">
      <SearchButton />
    </div>
</div>