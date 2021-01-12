<script>
    import { quaggaClosed } from "../stores/quaggaStore.js";
    import searchIcon from "../../public/icons/search-solid.svg";
    import timesIcon from "../../public/icons/times-solid.svg";

    let quaggaState; // 0 - off/ 1 - on

    quaggaClosed.subscribe(value => {
        quaggaState = value 
    });

    function changeQuagga() {
        (quaggaState == 0) ? quaggaClosed.set(1) : quaggaClosed.set(0);
    }

    function clickHandler() {
        changeQuagga();
    }
</script>

<style>
    button[type="button"] {
        border: none;
        height: 70px;
        width: 70px;
        background-color: #A3DDF0;
        color: black;
        padding: 20px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        margin: 4px 2px;
        border-radius: 50%;
    }
    img.search-icon {
        color: black;
        height: 30px;
    }
</style>

<button type="button" on:click={() => {clickHandler()}}>
    <img class="search-icon" src={quaggaState ? searchIcon : timesIcon} alt="search button">
</button>