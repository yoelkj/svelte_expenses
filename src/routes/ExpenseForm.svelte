<script>

    import Title from "./Title.svelte";
    
    export let addExpense;
    
    let name = '';
    let amount = null;


    //$: console.log({name, amount})

    $: isEmpty = !name || !amount;

    function handleSubmit(e){ 
        
        addExpense({name, amount});

        name = '';
        amount = null;
    }

</script>

<section class="form">
    
    <Title title="Add dExpense" />
    
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>

        <div class="form-control">
            <label for="name">Name</label>
            <input type="text" id="name" bind:value={name} />
        </div>

        <div class="form-control">
            <label for="amount">Amount</label>
            <input type="number" id="amount" bind:value={amount}/>
        </div>

        {#if isEmpty}
        <p class="form-empty">
            Please fill out form fields
        </p>
        {/if}

        <button type="submit" class="btn btn-block {isEmpty ? 'disabled' : ''} " disabled={isEmpty}>
            Add expense
        </button>

        <button type="button" class="close-btn">
            <i class="fas fa-times"></i>
            Close
        </button>

    </form>

</section>