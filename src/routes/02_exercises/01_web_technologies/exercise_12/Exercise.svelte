<script>
	let clicked = false;
</script>

<div>
	<button class="btn btn-primary" on:click={() => (clicked = true)}>
		click here
	</button>
	<!--  -->
	{#if clicked}
	You clicked on the button
	<!--clicked = false;-->
	{:else}
	You have to click on the button
	{/if}
</div>
