
<script>
    
    //Context
    import { afterUpdate, onMount, setContext } from 'svelte';

    //Componnets
    import Header from './Header.svelte';
    import ExpenseList from './ExpenseList.svelte';
    import Totals from './Totals.svelte';
    import ExpenseForm from './ExpenseForm.svelte';
    import Modal from './Modal.svelte';
    //Data
    //import import_rows from './expenses'; 
    import expenses from './expenses';
    
    let isFormOpen = false;

    //let data = [...import_rows];
    let data = [];
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
        showForm();
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
            return item.id === setId ? {...item, name, amount:amount}: {...item}
        });
        
        setId = null;
        setName = '';
        setAmount = null;

        
    }

    function showForm(){
		isFormOpen = true;
	}
    function closeForm(){
		isFormOpen = false;
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


    //Local storage
    function setLocalStorage(){
        localStorage.setItem('expenses', JSON.stringify(data))
    }

    onMount(() =>{
        data = localStorage.getItem('expenses') ? JSON.parse(localStorage.getItem('expenses')) : [];
        console.log(data);
    });

    afterUpdate(() => {
        setLocalStorage();
    })


</script>

<!--
<ExpenseList rows={data} on:delete={deleteExpense} />
-->


<Header {showForm}/>

<main class="content">
	
    {#if isFormOpen}
    <Modal>
        <ExpenseForm 
            {editExpense} 
            {addExpense} 
            {closeForm}
            {isEditing} 
            name={setName} 
            amount={setAmount} /> 
    </Modal>
    {/if}

    <Totals title="Total expenses" total="{total}" />

    <ExpenseList rows={data} />

    <button on:click={clearExpenses} class="btn-primary btn-block">
        Clear expenses
    </button>
</main>
<!--
    <Modal>
        <h2 slot="header">Header content</h2>
        <p slot="footer">Footer content</p>
    </Modal>
-->
