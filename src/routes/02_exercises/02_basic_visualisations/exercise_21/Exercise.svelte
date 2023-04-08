<script>
    import Scatterplot from './Scatterplot.svelte';
    import {onMount} from 'svelte';
    import {json} from 'd3-fetch';

    //let data_app = 8;

    /*let test = [{id:22, name: "lana"},
    {id:33,name:"John"},
    {id:45,name:"avril"}];

    let select_test = test.filter(users => users.id==22);

    console.log(select_test[0].name)*/

    let data_app = null;
    let loaded = false;
    onMount(async () => {
        console.log("onMount started!");
        //data_app=5;

        data_app = await json('/data/gapminder.json');
        data_app = data_app.filter(cell => cell.year==1800);
        data_app = data_app[0].countries;
        //data_app = data_app.countries;
        loaded = true;
        //data_app = 10;
        console.log("onMount finished")
        /*data_app = await csv('/myFile.csv');
        console.log("Data loaded!");*/
  });
  console.log("Script finished!")

</script>

{#if loaded}
    <Scatterplot data_scatter={data_app} loaded_scatter={loaded}/>
{/if}