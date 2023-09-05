<script>
    import Title from "./Title.svelte";
    import Expense from "./Expense.svelte";
  import { fly } from "svelte/transition";
  import { flip } from "svelte/animate";
  import { quintOut } from "svelte/easing";

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
        {#each rows as expense, index (expense.id)}
                <!-- <Expense {...expense} on:delete/> -->
                <li 
                out:fly={{x:-200}} 
                in:fly={{x:200, delay:(index+1)*700}}
                animate:flip={{ delay: 250, duration: 250, easing: quintOut }}
                    >

                    <Expense {...expense}  />
                
                </li>
             
        {:else}
            <h2>No expenses added to the list.</h2>   
        {/each}
    </ul>
</section>