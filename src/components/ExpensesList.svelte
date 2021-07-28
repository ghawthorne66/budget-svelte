<script>
    import Title from "./Title.svelte"
    import SingleExpense from "./SingleExpense.svelte"
    export let expenses = [];


</script>
<style>
    h2{
        text-transform: capitalize;
    }
</style>

<section>
    <Title title="expenses list"/>
    <ul>
        {#each expenses as expense, index}
            <SingleExpense {...expense} />
            {:else}
            <h2>no expenses added to the list</h2>

        {/each}

    </ul>
</section>