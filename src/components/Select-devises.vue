<template>
        <div class="form-group mb-2">
            <select  name="devise1" id="devise1" v-model="key1">
                <option @click="choice1()" value="EUR">EUR</option>
                <option @click="choice1()" :value="index" :key="index" v-for="(devise,index) in devises"> {{index}}</option>
            </select>
            <span> TO </span>
            <select  name="devise2" id="devise2" v-model="key2">
                <option @click="choice2()" value="EUR">EUR</option>
                <option @click="choice2()" :value="index" :key="index" v-for="(devise,index) in devises"> {{index}}</option>
            </select>
        </div>

</template>


<script>
    export default {
        props: ['devises'],
        name: 'Select-devises',
        emits: ["choixUno","choixDos"],
        data(){
            return {
                key1: '',
                key2: '',
                rates: []
            }
        },
        methods: {
            choice1: function(){
                this.$emit('choixUno', this.key1)
            },
            choice2(){
                this.$emit('choixDos', this.key2)
            }
        },
        mounted(){
            //this.rates.push(this.devises);
            console.log(this.devises);
            //this.rates.unshift({'EUR': 0})
        },
    }
</script>


<style>

</style>