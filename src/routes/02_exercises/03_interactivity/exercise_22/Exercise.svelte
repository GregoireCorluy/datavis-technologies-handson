<script>

    let counter = 0;

    function Increase(event) {
        counter++;
    console.log("Clicked Increase!");
    }
    
    function Reset(event) {
        counter = 0;
        console.log("Clicked Reset!");
    }
</script>

Number of times clicked: {counter}.
<br/>
<button on:click={Increase}>Increase</button>
<br/>
<button on:click={Reset}>Reset</button>

<style>
    button{
        border-radius:6px;
        background-color: red;
        color:rgb(239, 231, 5);
        font-weight:bold;
        margin-top: 0.3em;
        margin-bottom: 0.3em;
    }
</style>