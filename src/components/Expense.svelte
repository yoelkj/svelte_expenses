<script>
    
    import {getContext, setContext} from 'svelte';

    export let name = "";
    export let amount = 0;
    export let id = 0;

    let displayAmount = false;

    function toggleAmount(){
        displayAmount = !displayAmount;
    }

    const {remove} = getContext('state');
    
</script>

<li>
    <article class="single-expense">
        <div class="expense-info">
            <h2>
                {name}  
                <button class="amount-btn" on:click="{toggleAmount}">
                    <i class="fas fa-caret-down"></i> 
                </button>
            </h2>
            {#if displayAmount}
                <h4>Amount: ${amount}</h4>
            {/if}
            
        </div>

        <div class="expense-buttons">
            <button class="expense-btn edit-btn">
                <i class="fas fa-pen"></i>
            </button>

            <button class="expense-btn delete-btn" on:click="{() => remove(id)}">
                <i class="fas fa-trash"></i>
            </button>
        </div>
        
        
    </article>
</li>