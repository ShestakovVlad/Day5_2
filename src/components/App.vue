<template>
   <div >
       <h1 align='center'> Погода</h1>
       <table align='center'>
           <tr>
               <td style="border:none"><input type="text" v-model="Add">
                    <br><button v-on:click="add">Добавить город</button></td>
                <td style="border:none; min-width:50px"> <select v-model="city" style="min-width:150px">
                        <option  v-for="city in Nciti" v-bind:key="city" v-bind:value="city">{{city}}</option>
                    </select>
                    <br><button v-on:click="get">Узнать погоду</button>
                </td>
            </tr>
       </table  >
       <table style="font-size:24px" align='center' v-if="weather.cod  >0">
                <tr valign  > <img src="/components/oblako.jpg" width="20" > Страна: {{weather.sys.country}}</tr>
                <tr valign > <img src="/components/i.jpg" width="20">Город: {{city}}</tr>    
               <tr valign > <img src="/components/2.jpg" width="30">Температура: {{weather.main.temp | round}} K</tr>
               <tr valign > <img src="/components/2.jpg" width="30">Чувствуется как: {{weather.main.feels_like | round}} K</tr>
               <tr valign > <img src="/components/2.jpg" width="30">Минимальная: {{weather.main.temp_min | round}} K</tr>
               <tr valign > <img src="/components/2.jpg" width="30">Максимальная: {{weather.main.temp_max | round}} K</tr>
               <tr valign > <img src="/components/3.jpg" width="30">Скорость ветра: {{weather.wind.speed}}</tr>
            
       </table>
       
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
           Add:"",
           city:"",
           Nciti:[],
           weather:[],
           testValue:0,
           dolg:0,
           shir:0,

        }},
        mounted: function(){
            
               
               if(localStorage.getItem("Nciti") !== '') this.Nciti = JSON.parse(localStorage.getItem("Nciti")|| "[]");
               
            
        },
        methods:{
            
        
            get: function() {
                 axios.get("https://api.openweathermap.org/data/2.5/weather?q="+this.city+"&appid=7914d5a440960cfd5df3bd0388a7ad0f", {
                          units: "metric",
                })
                .then((response)=>{
                    console.log(response.data);
                    this.weather = response.data;
                    
                })
            },
            add: function(){
                this.Nciti.push(this.Add)
                localStorage.setItem("Nciti",JSON.stringify(this.Nciti))
            },
            
        },
        filters:{
            round: function(value){
                return parseFloat(value.toFixed(1));
            },
        }
        
    }
</script>
<style scoped>

</style>