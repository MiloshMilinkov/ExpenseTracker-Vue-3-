<template>
    <div>
        <h3>Add new transaction</h3>
        <form id="form" @submit.prevent="onSubmit">
            <div class="form-control">
                <label for="text">Text</label>
                <input type="text" id="text" placeholder="Enter text..." v-model="text">
            </div>
            <div class="form-control">
                <label for="amount">
                    Amount <br> (negative - epxense, positive - income)
                </label>
                <input type="text" id="amount" placeholder="Enter amount..." v-model="amount">
            </div>
            <button class="btn">Add transaction</button>
        </form>
    </div>
</template>

<script setup>
    import { ref } from 'vue';
    import { useToast } from 'vue-toastification';


    const text = ref('');
    const amount = ref('');

    const toast = useToast();

    const onSubmit = () =>{
        if( !text.value && !amount.value){
            toast.error('Both fields must be filled.');
            return;
        }
        else if( !amount.value){
            toast.error('Amount field must be filled.');
            return;
        }
        else if( !text.value ){
            toast.error('Text field must be filled.');
            return;
        }

        const transactionData = {
            text: text.value,
            amount: parseFloat(amount.value)
        }

        emit('transactionSubmited', transactionData);
        
        text.value = '';
        amount.value = '';
    }

    const emit = defineEmits(['transactionSubmited']);
</script>