<script>
    
    //import { blur, scale, slide, fade, fly } from "svelte/transition";
    
    import { fly, slide } from "svelte/transition";
    import { getContext } from "svelte";

    export let id;
    export let name ='';
    export let amount = 0;

    let display_amount = false;

    function toggleAmount(){
        display_amount = !display_amount;
    }

    const {remove, modify} = getContext('state');

    //const dispatch = createEventDispatcher();    
    
</script>

<article iden="iden-{id}" class="single-expense">
    
    <div class="expense-info">

        <h2>{name} <button class="amount-btn" on:click={toggleAmount}><i class="fas fa-caret-down"></i> more..</button> </h2>
        {#if display_amount }
            <!--<h4 transition:blur>Amount: ${amount}</h4>-->
            <!--<h4 transition:scale>Amount: ${amount}</h4>-->
            <h4 transition:slide>Amount: ${amount}</h4>
            <!--<h4 transition:fade>Amount: ${amount}</h4>-->
            <!--<h4 transition:fly>Amount: ${amount}</h4>-->
            <!--<h4 in:fly out:slide>Amount: ${amount}</h4>-->
        {/if}
    </div>

    <div class="expense-buttons">
        <!--
        <button class="expense-btn delete-btn" on:click={ () => dispatch('delete', {id, name: 'Hello from expense'}) }><i class="fas fa-trash"> Del</i></button>
        -->
        <button class="expense-btn edit-btn" on:click={() => modify(id)}><i class="fas fa-pen"> Edit</i></button>
        <button class="expense-btn delete-btn" on:click={ () => remove(id) }><i class="fas fa-trash"> Del</i></button>
    </div>
</article>