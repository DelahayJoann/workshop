<template>
    <div class="container">
        <h1 class="my-4">App Meteo avec Vue.js</h1>
        <div class="form-group mb-5">
            <label for="position">Entrez le nom d'une ville</label>
            <select name="test" id="test">
                <option value="`{{index}}`" :key="index" v-for="(devise,index) in devises_rate"> {{index}}</option>
            </select>
        </div>

        <div class="w-75 m-auto">
            <h3 class="text-center mb-3">Position:

            </h3>
            <div class="card text-center p-5">
                <p class="texte-affichage">

                </p>
                <p class="texte-affichage">

                </p>
            </div>
        </div>
    </div>
</template>


<script>
    import axios from 'axios'
    export default {
        name: 'Exchange',
        data(){
            return {
                requete: '',
                devises_rate: [],
                url_latest: 'https://api.exchangeratesapi.io/latest',
                url_convert: 'https://api.exchangeratesapi.io/latest?symbols=' //USD,GBP
            }
        },
        methods: {
            
        },
        created(){
            axios
            .get(`${this.url_latest}`)
            .then(reponse => {
                console.log(reponse);
                this.devises_rate = reponse.data.rates;
            })
        }
    }
</script>


<style>
.texte-affichage {
    font-size: 30px;
    font-weight: 300;
    line-height: 1.2;
}
</style>