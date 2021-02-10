<template>
    <div class="container">
        <h1 class="my-4">App Exchange</h1>
        <select-devises v-bind:devises="devises_rates" v-on:choixUno="choixUn($event)" v-on:choixDos="choixDeux($event)"></select-devises>
        <amount-input v-on:amountSend="receiveAmount($event)" v-model="amount"></amount-input>
        <p class="converted">{{ out }}</p>
    </div>
</template>


<script>
    import axios from 'axios';
    import SelectDevises from './Select-devises.vue';
    import AmountInput from './Amount-input.vue';
    export default {
        name: 'Exchange',
        data(){
            return {
                devise1: '',
                devise2: '',
                amount: 0,
                devises_rates: [],
                convert_rate: undefined,
                converted: 0,
                url_latest: 'https://api.exchangeratesapi.io/latest',
                url_convert_rate: 'https://api.exchangeratesapi.io/latest?base='
            }
        },
        methods: {
            choixUn: function(devi){
                this.devise1 = devi;
                if(this.devise1 && this.devise2)this.receiveAmount(this.amount);
            },
            choixDeux: function(devi){
                this.devise2 = devi;
                if(this.devise1 && this.devise2)this.receiveAmount(this.amount);
            },
            receiveAmount: function(amount){
                this.amount = amount;
                this.getRate(this.url_convert_rate+this.devise1+'&symbols='+this.devise2, amount)
            },
            getRate: function(url,amount){
                axios
                .get(url)
                .then(reponse =>{
                   this.convert_rate = reponse.data.rates;
                   this.converted = amount * this.convert_rate[this.devise2];
                })
            },
        },
        components: { SelectDevises, AmountInput },
        created(){
            axios
            .get(`${this.url_latest}`)
            .then(reponse => {
                this.devises_rates = reponse.data.rates;
            })
        },
        computed: {
                out: function(){
                    let output = '';
                    output += (this.devise1)?this.amount+' '+this.devise1+' = ':'? = ';
                    output += (this.devise2)?this.converted.toFixed(2)+' '+this.devise2:' ?';
                    return  output;
                }
            }
    }
</script>


<style>
.converted{
    font-size: 20px;
}
</style>