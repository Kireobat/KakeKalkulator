<script lang="ts">
    let cakeMixList = [
        {
            name: 'Sjokoladekake Langpanne',
            id: 0,
            height: 30,
            width: 40,
            price: 65.90,
            weight: 854,
            butterNeeded: 200,
            stykker: 24
        },
        {
            name: 'Brownie Langpanne',
            id: 1,
            height: 30,
            width: 40,
            price: 57.90,
            weight: 883,
            butterNeeded: 150,
            eggNeeded: 2,
            stykker: 20
        },
        {
            name: 'Brownie',
            id: 2,
            height: 20,
            width: 30,
            price: 32.50,
            weight: 552,
            butterNeeded: 100,
            eggNeeded: 1,
            stykker: 12
        }

    ]

    let butterList = [
        {
            name: 'Bremykt Mykere',
            id: 0,
            price: 47.90,
            weight: 500
        },
        {
            name: 'Brelett',
            id: 1,
            price: 39.90,
            weight: 540
        },
        {
            name: 'Tine Meierismør',
            id: 2,
            price: 56.50,
            weight: 500
        },
        {
            name: 'Melange Original',
            id: 3,
            price: 36.90,
            weight: 500
        },
        {
            name: 'Melange Flytende m/Smør',
            id: 4,
            price: 38.90,
            weight: 500
        },
        {
            name: 'Melange Flytende Smør/Rapsolje',
            id: 5,
            price: 36.70,
            weight: 500
        },
        {
            name: 'Melange Original 1kg',
            id: 6,
            price: 68.90,
            weight: 1000
        }
    ]

    let eggList = [ 
        {
        name: "FirstPrice Egg",
        id: 0,
        price: 47.40,
        amount: 18
        },

]

    let stykkeBuyPrice = 0;

    let selectedCakeMixIndex = 0;
    let selectedButterIndex = 0;
    let selectedEggIndex = 0;

    let cakeMixPrice = 0;
    let cakeMixWeight = 0;
    let cakeMixPricePerGram = 0;
    let cakeMixButterNeeded = 0;
    let cakeMixEggNeeded: any = 0;
    let cakeHeight = 0;
    let cakeWidth = 0;
    let cakeStykker = 0;

    let butterPrice = 0;
    let butterWeight = 0;
    let butterPricePerGram = 0;

    let eggPrice = 0;
    let eggAmount = 0;


    $: {
        cakeMixPrice = cakeMixList[selectedCakeMixIndex].price;
        cakeMixWeight = cakeMixList[selectedCakeMixIndex].weight;
        cakeMixPricePerGram = cakeMixPrice / cakeMixWeight;
        cakeMixButterNeeded = cakeMixList[selectedCakeMixIndex].butterNeeded;
        cakeMixEggNeeded = cakeMixList[selectedCakeMixIndex].eggNeeded;
        cakeHeight = cakeMixList[selectedCakeMixIndex].height;
        cakeWidth = cakeMixList[selectedCakeMixIndex].width;
        cakeStykker = cakeMixList[selectedCakeMixIndex].stykker;

        butterPrice = butterList[selectedButterIndex].price;
        butterWeight = butterList[selectedButterIndex].weight;
        butterPricePerGram = butterPrice / butterWeight;

        eggPrice = eggList[selectedEggIndex].price;
        eggAmount = eggList[selectedEggIndex].amount;
    }
</script>


<select bind:value={selectedCakeMixIndex}>
    {#each cakeMixList as cakeMix}
        <option value={cakeMix.id}>{cakeMix.name}</option>
    {/each}
</select>

<select bind:value={selectedButterIndex}>
    {#each butterList as butter}
        <option value={butter.id}>{butter.name}</option>
    {/each}
</select>

{#if selectedCakeMixIndex == 1 || selectedCakeMixIndex == 2}
<select bind:value={selectedEggIndex}>
    {#each eggList as egg}
        <option value={egg.id}>{egg.name}</option>
    {/each}
</select>
{/if}

<input type="number" bind:value={stykkeBuyPrice} placeholder="Stykke buy price"/>

<br/>
<br/>
<div class="flex flex-col">
<h1>Data about the selected cakemix:</h1>
<h1>Name: {cakeMixList[selectedCakeMixIndex].name}</h1>
<h1>Price: {cakeMixPrice}</h1>
<h1>Weight: {cakeMixWeight}</h1>
<h1>NOK per g: {cakeMixPricePerGram}</h1>
<h1>Butter needed: {cakeMixButterNeeded}</h1>
{#if selectedCakeMixIndex == 1 || selectedCakeMixIndex == 2}
<h1>Egg needed: {cakeMixEggNeeded}</h1>
{/if}
<h1>Height: {cakeHeight}</h1>
<h1>Width: {cakeWidth}</h1>
<h1>Stykker: {cakeStykker}</h1>
</div>

<br/>
<div class="flex flex-col">
<h1>Data about the selected butter:</h1>
<h1>Name: {butterList[selectedButterIndex].name}</h1>
<h1>Price: {butterPrice}</h1>
<h1>Weight: {butterWeight}</h1>
<h1>NOK per g: {butterPricePerGram}</h1>
</div>

<br/>

<div class="flex flex-col">
    <h1>Startup Data</h1>
    {#if selectedCakeMixIndex == 1 || selectedCakeMixIndex == 2}
    <h1>Startup cost: {cakeMixPrice+butterPrice+eggPrice}</h1>
    {:else}
    <h1>Startup cost: {cakeMixPrice+butterPrice}</h1>
    {/if}
    <h1>Nok smør til {butterWeight/cakeMixButterNeeded} kaker</h1>
    {#if selectedCakeMixIndex == 1 || selectedCakeMixIndex == 2}
    <h1>Nok egg til {eggAmount/cakeMixEggNeeded} kaker</h1>
    {/if}
</div>

<br/>

<div class="flex flex-col">
    <h1>Prod data</h1>
    {#if selectedCakeMixIndex == 1 || selectedCakeMixIndex == 2}
    <h1>Gjennomsnitt pris per kake: {cakeMixPrice + ((butterPrice/(butterWeight/cakeMixButterNeeded))+ (eggPrice/(eggAmount/cakeMixEggNeeded)))}</h1>
    <h1>Kostnad per stykke: {(cakeMixPrice + ((butterPrice/(butterWeight/cakeMixButterNeeded))+ (eggPrice/(eggAmount/cakeMixEggNeeded))))/cakeStykker}</h1>
    <h1>Profit per stykker: {stykkeBuyPrice - (cakeMixPrice + ((butterPrice/(butterWeight/cakeMixButterNeeded))+ (eggPrice/(eggAmount/cakeMixEggNeeded))))/cakeStykker}</h1>
    <h1>Profit per kake: {(stykkeBuyPrice - (cakeMixPrice + ((butterPrice/(butterWeight/cakeMixButterNeeded))+ (eggPrice/(eggAmount/cakeMixEggNeeded))))/cakeStykker)*cakeStykker}</h1>
    {:else}
    <h1>Gjennomsnitt pris per kake: {cakeMixPrice + (butterPrice/(butterWeight/cakeMixButterNeeded))}</h1>
    <h1>Kostnad per stykke: {(cakeMixPrice + (butterPrice/(butterWeight/cakeMixButterNeeded)))/cakeStykker}</h1>
    <h1>Profit per stykke: {stykkeBuyPrice - (cakeMixPrice + (butterPrice/(butterWeight/cakeMixButterNeeded)))/cakeStykker}</h1>
    <h1>Profit per kake: {(stykkeBuyPrice - (cakeMixPrice + (butterPrice/(butterWeight/cakeMixButterNeeded)))/cakeStykker)*cakeStykker}</h1>
    {/if}



</div>