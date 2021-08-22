<script>
    import {setContext} from 'svelte';

    const state = {
        name: 'Simple name',
        remove: handleRemoveExpense
    }

    import Navbar from "./components/Navbar.svelte";
    import ExpenseList from "./components/ExpenseList.svelte";
    import ExpensesData from "./expenses";
    
    let expenses = [...ExpensesData];

    function handleRemoveExpense(id){
        expenses = expenses.filter(item => item.id !== id);
    }

    setContext('state', state);

</script>

<Navbar/>
<main class="content">
    <ExpenseList {expenses}/>
</main>