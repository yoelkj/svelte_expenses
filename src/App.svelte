<script>

    import Navbar from "./components/Navbar.svelte";
    import ExpenseList from "./components/ExpenseList.svelte";
    import ExpensesData from "./expenses"

    let expenses = [...ExpensesData];

    function handleRemoveExpense(id){
        expenses = expenses.filter(item => item.id !== id);
        
    }
</script>

<Navbar/>
<ExpenseList {expenses} {handleRemoveExpense}/>


