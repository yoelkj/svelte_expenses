
<script>
    import Expense from "./Expense.svelte";
    import Title from "./Title.svelte";
    
    export let expenses = [];
    export let handleRemoveExpense;

</script>
<style>
    h2{
        text-transform: uppercase;
    }
</style>

<section>

    <Title title="Expenses list"></Title>   

</section>
<ul>
    {#each expenses as expense, index}
        
    <Expense {...expense} {handleRemoveExpense}></Expense>
    {:else}
         <!-- else content here -->
         <h2>No rows</h2>
    {/each}
</ul>