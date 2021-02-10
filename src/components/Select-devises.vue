<template>
        <div class="form-group mb-2">
            <select  name="devise1" id="devise1" v-model="key1">
                <option @click="choice1()" value="EUR" v-if="key2 != 'EUR'">EUR</option>
                <option @click="choice1()" :value="index" :key="index" v-for="(devise,index) in devises"> {{index}}</option>
            </select>
            <span> TO </span>
            <select  name="devise2" id="devise2" v-model="key2">
                <option @click="choice2()" value="EUR" v-if="key1 != 'EUR' && key1" >EUR</option>
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
            },
        },
    }
</script>


<style>

</style>