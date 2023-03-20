<script>
    //let hobbies_list = ["golf","chess","cycling","math","physics"];
    let GregList = {name:"Grégoire Corluy",
                hobbies:["golf","chess","cycling","math","physics"]};
</script>

My name is {GregList.name} and these are some of my favourite things:
<ul>
    {#each GregList.hobbies as elements}
        <li>{elements}</li>
    {/each}
</ul>