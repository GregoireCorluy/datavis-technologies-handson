<script>
	const videos = [
		{ url: 'https://www.youtube.com/watch?v=S4bn6gg-BmE', name: 'Messi' },
		{ url: 'https://www.youtube.com/watch?v=MD6WXsjdcsY', name: 'Ronaldo' },
		{ url: 'https://www.youtube.com/watch?v=yTGr45ZQRdA', name: 'Neymar' }
	];
</script>

<div>
	<h5>Famous soccer players:</h5>
	<ul>  <!--<ul style="list-style-type:georgian">-->
	{#each videos as player}
		<li> {player.name}: <a href={player.url}> {player.url}</a> </li>
	{/each}
	</ul>
		
</div>

<style>
li {
	list-style-type: none;
	position: relative;
	padding-left: 15px;
  }
  
  li:before {
	content: "\25BA \0020";
	font-size: 10px;
	position: absolute;
	top: 5px;
	left: -0px;
  }
</style>