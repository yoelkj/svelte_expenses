<script>
    import Title from "./Title.svelte";
    import Expense from "./Expense.svelte";
  import { fly } from "svelte/transition";

    export let rows = [];
</script>
<style>
    h2{
        text-transform: capitalize;
    }
</style>
<section>
    
    <Title title="Expense List" />

    <ul>
        {#each rows as expense, index}
            <li>
                <!-- <Expense {...expense} on:delete/> -->
                <div transition:fly={{x:200, delay:(index+1)*700}}> 
                    <Expense {...expense}  />
                </div>
            </li> 
        {:else}
            <h2>No expenses added to the list.</h2>   
        {/each}
    </ul>
</section>