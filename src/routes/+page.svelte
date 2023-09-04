
<script>
    
    //Context
    import { setContext } from 'svelte';
    //Componnets
    import ExpenseList from './ExpenseList.svelte';
    import Totals from './Totals.svelte';
    import ExpenseForm from './ExpenseForm.svelte';
    //Data
    import import_rows from './expenses'; 
  import expenses from './expenses';
    
    let data = [...import_rows];
    
    $: total = expenses.reduce((acc, curr) => {
        //console.log({acc, amount: curr.amount})
        return (acc += curr.amount)
    }, 0);

    const state = {
        param: 'Param example',
        remove: removeExpense
    }

    function removeExpense(id) {
        console.log(id);
        data =  data.filter(item => item.id !== id);
    }
    function clearExpenses(){
        data = [];
    }

    function addExpense({name, amount}){
        //console.log({name, amount});
        let expense = {
            id: Math.random() * Date.now(),
            name, 
            amount
        }

        data = [expense, ...data];
        
        console.log(data);
    }

    setContext('state', state);

    /*
    function deleteExpense(event){
        const {id, name} = event.detail;
        console.log(name);
        removeExpense(id);
    }
    */

</script>

<!--
<ExpenseList rows={data} on:delete={deleteExpense} />
-->

<ExpenseForm {addExpense} />

<Totals title="Total expenses" total="{total}" />

<ExpenseList rows={data} />

<button on:click={clearExpenses} class="btn-primary btn-block">
    Clear expenses
</button>

