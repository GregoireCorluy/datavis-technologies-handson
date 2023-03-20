<script>
    let numbers = [0, 5, 10, 15, 20, 25];
</script>


<div>
    {#each numbers as num, i(num)}
    <p style = "font-size: {50-num}px"> Header {i+1} </p>
    {/each}
 </div>