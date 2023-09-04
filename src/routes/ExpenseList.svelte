<script>
    import Title from "./Title.svelte";
    import Expense from "./Expense.svelte";

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
        {#each rows as expense}
            <li>
                <!-- <Expense {...expense} on:delete/> -->
                <Expense {...expense} />
            </li> 
        {:else}
            <h2>No expenses added to the list.</h2>   
        {/each}
    </ul>
</section>