<script>
    // import {toggleAmount} from "../functions"
    import {getContext} from 'svelte';

    export let id, name = '', amount = 0;
    let displayAmount = false;

    function toggleAmount() {
        displayAmount = !displayAmount;
    }

    const removeExpense = getContext('remove');
    const setModifiedExpense = getContext('modify');
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>{name}
            <button class="amount-btn" on:click|once={toggleAmount}>
                <i class="fas fa-caret-down"></i>
            </button>
        </h2>
        {#if displayAmount}
            <h4>amount : ${amount}</h4>
        {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-btn edit-btn" on:click={() => setModifiedExpense(id)}>
            <i class="fas fa-pen"></i>
        </button>
        <button class="expense-btn delete-btn"
                on:click={() => removeExpense(id)}>
            <i class="fas fa-trash"></i>
        </button>


    </div>
</article>