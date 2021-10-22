<template>
<div>
    <select v-model="branch" v-on:click = handleCityChoosing>
        <option  v-for="citi in cities" :key="citi.CityID" :value="citi.Description">   
            {{citi.Description}}
        </option>
    </select>

    <select   >
        <option  v-for="branch in branches" :key="branch.CitiCityID" :value="branch.Description">   
            {{branch.Description}}
        </option>
    </select>

   
   </div>
</template>

<script>
    
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'


    export default {
    data: function() {
        return {
        cities:[],
           branches:[],
           branch:"---------",
            
        
    }},
    mounted: function(){
        axios.post("https://api.novaposhta.ua/v2.0/json/Address/getCities", {
            
        apiKey: "a296ca247f95d5c0d9755e9b97b2e6a4",
        modelName: "Address",
        calledMethod: "getCities",
        methodProperties: {}
        })
        .then((response)=>{
        console.log(response.data);
        this.cities = response.data.data;
        })

    },
    methods:{

        handleCityChoosing: function() {
                
                 axios.post("https://api.novaposhta.ua/v2.0/json/Address/getWarehouses", {
                        apiKey: "a296ca247f95d5c0d9755e9b97b2e6a4",
                        modelName: "Address",
                        calledMethod: "getWarehouses",
                        methodProperties: {CityName: this.branch}
                })
                .then((response)=>{
                    console.log(response.data);
                    this.branches = response.data.data;
                })
            }

    }
    }
    
</script>
