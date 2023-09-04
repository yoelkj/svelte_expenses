
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
   
    
    let setName = '';
    let setAmount = null;
    let setId = null;

    $: isEditing = setId ? true : false;
    $: total = expenses.reduce((acc, curr) => {
        //console.log({acc, amount: curr.amount})
        return (acc += curr.amount)
    }, 0);

    const state = {
        param: 'Param example',
        remove: removeExpense,
        modify: setModifiedExpense
    }

    setContext('state', state);

    function removeExpense(id) {
        console.log(id);
        data =  data.filter(item => item.id !== id);
    }
    function clearExpenses(){
        data = [];
    }

    function setModifiedExpense(id){
        let expense = data.find(item => item.id === id);
        setName = expense.name;
        setAmount = expense.amount;
        setId = expense.id;
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

    function editExpense({name, amount}){
        data = data.map(item => {
            return item.id = setId ? {...item, name, amount:amount}: {...item}
        });
        setId = null;
        setName = '';
        setAmount = null;
    }

    

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

    <ExpenseForm {editExpense} {addExpense} {isEditing} name={setName} amount={setAmount}/> 

    <Totals title="Total expenses" total="{total}" />

    <ExpenseList rows={data} />

    <button on:click={clearExpenses} class="btn-primary btn-block">
        Clear expenses
</button>
