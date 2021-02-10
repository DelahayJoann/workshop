<template>
        <div class="form-group mb-2">
            <label for="position">Montant:</label>
            <input @input="amountSended()" type="number" name="amount" id="amount" v-model="amount">
        </div>
</template>


<script>
    export default {
        name: 'Amount-input',
        emits: ["amountSend"],
        data(){
            return {
                amount: 0,
            }
        },
        methods: {
            amountSended: function(){
                this.$emit('amountSend', this.amount)
            },
        },
        created(){

        }
    }
</script>


<style>
#amount{
    display: block;
}
</style>