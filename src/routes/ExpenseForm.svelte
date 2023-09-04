<script>
    
    //import { onMount,
    //         onDestroy,
    //         beforeUpdate, 
    //         afterUpdate } from "svelte";
    //
    //onMount(() => {console.log('form has mounted');    })
    //beforeUpdate(() => {console.log('Before updated');    })
    //afterUpdate(() => {console.log('After updated');    })
    //onDestroy(() => {console.log('form has hidden');    })

    import Title from "./Title.svelte";
    
    export let addExpense;
    export let editExpense;
    export let closeForm;
    
    
    export let name = '';
    export let amount = null;
    export let isEditing;


    //$: console.log({name, amount})

    $: isEmpty = !name || !amount;

    function handleSubmit(e){ 
        
        if(isEditing){
            editExpense({name, amount});
        }else{
            addExpense({name, amount});
        }
        

        name = '';
        amount = null;
        closeForm();
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

        <button type="submit" class="btn btn-block" class:disabled={isEmpty} disabled={isEmpty}>
            {#if isEditing}
                Edit expense
            {:else}
                Add expense
            {/if}
        </button>

        <button type="button" class="close-btn" on:click={closeForm}>
            <i class="fas fa-times"></i>
            Close
        </button>

    </form>

</section>