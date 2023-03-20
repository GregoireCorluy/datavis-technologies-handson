<script>
  let current = "";
</script>

<!-- We will cover buttons later on! -->
<button class="btn btn-secondary" class:primary={current==="messi"} on:click={() => (current = "messi")}>
  Messi
</button>

<button class="btn btn-secondary" class:primary={current==="ronaldo"} on:click={() => (current = "ronaldo")}>
  Ronaldo
</button>

<button class="btn btn-secondary" class:primary={current==="neymar"} on:click={() => (current = "neymar")}>
  Neymar
</button>

<style>
  button{
    background:red
  }
  .primary{
    background:green
  }
  </style>