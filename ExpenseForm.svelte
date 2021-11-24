<script>
   // import {onMount,onDestroy,beforeUpdate,afterUpdate} from 'svelte';
   /* onMount(()=>{
       console.log("form has mounted");
    });
    onDestroy(()=>{
       console.log("form is hidden");
    });
    afterUpdate(()=>{
       console.count("form has mounted");
    });
    beforeUpdate(()=>{
       console.count("form has mounted");
    });*/
    import Title from './Title.svelte';
    export let name='';
    export let amount = null;
    export let addExpense;
    export let isEditing;
    export let editExpense;
    export let hideForm;
   // $:console.log({name,amount});
   $: isEmpty = !name || !amount;
   function handleSubmit(){
       if(isEditing){
           editExpense({name,amount});
       }
       else{
        addExpense({amount,name});
       }
       name = '';
       amount = null;
       hideForm();
   }
</script>
<section class="form">
    <Title title ="add expense"/>
    <form  class="expense-from" on:submit|preventDefault={handleSubmit}>
        <div class="form-control">
            <label for="name">Name</label>
            <input type="text" id="name" bind:value={name}>
        </div>
        <div class="form-control">
            <label for="amount">Amount</label>
            <input type="number" id="amount" bind:value={amount}>
        </div>
        {#if isEmpty}
        <p class="form-empty">
            Please fill out all form fields
        </p>
        {/if}
        <button type="submit" class="btn btn-block" class:disabled={isEmpty}>
            {#if isEditing} edit expense 
            {:else}add expense
            {/if}
        </button>
        <button type="button" class="close-btn" on:click={hideForm}>
            <i class="fas fa-times"></i>
            Close
           </button>
    </form>
</section>