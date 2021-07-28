<script>
    import {setContext} from 'svelte';
    import Navbar from "./components/Navbar.svelte";
    import ExpensesList from "./components/ExpensesList.svelte";
    import Totals from "./components/Totals.svelte"
    import ExpenseForm from "./components/ExpenseForm.svelte"
    import expensesData from "./expenses";
    //variables
    let expenses = [...expensesData];
    //set editing variables
    let setName = "";
    let setAmount = null;
    let setId = null;
    //reactive
    $: isEditing = setId ? true : false;
    $: total = expenses.reduce((acc, curr) => {
        // console.log({acc, amount: curr.amount})
        return (acc += curr.amount)
    }, 0)

    //functions
    function removeExpense(id) {
        expenses = expenses.filter(item => item.id
            !== id);
    }

    function clearExpenses() {
        expenses = [];
    }

    function addExpense({name, amount}) {
        let expense = {id: Math.random() * Date.now(), name, amount};
        expenses = [expense, ...expenses]
    }

    function setModifiedExpense(id) {
        let expense = expenses.find(item => item.id === id);
        setId = expense.id;
        setName = expense.name;
        setAmount = expense.amount;
    }

    function editExpense({name, amount}) {
        expenses = expenses.map(item => {
            return item.id === setId ? {...item, name, amount} : {...item}
        });
        setId = null;
        setAmount = null;
        setName = "";

    }

    //context
    setContext('remove', removeExpense);
    setContext('modify', setModifiedExpense);


</script>


<Navbar/>
<main class="content">
    <ExpenseForm {addExpense} name={setName} amount={setAmount} {isEditing} {editExpense}/>
    <Totals title="total expenses" {total}/>
    <ExpensesList {expenses}/>
    <button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>
        clear expenses
    </button>

</main>
