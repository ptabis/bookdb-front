<script>
    import { dataStore } from "../stores/dataStore.js";
    let title;

    dataStore.subscribe(value => {
        title = value.data.title;
    });
</script>

<style>
</style>

<div>
    {#if title}<p>{title}</p>{/if}
</div>