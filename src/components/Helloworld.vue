<template>
    <div class="main">
            <div class="weather-wrap">
                <div class="Search-box">
                    <input type="text" 
                    class="Search"
                    placeholder="Search..."
                    v-model="query"
                    @keypress="fetchweather"
                    />
                </div>
            </div>
        <div class="Weather-Data" v-if="typeof weather.main != 'undefined'">
            <div class="location">
                <div class="location-box">
                    <label class="country" for="Country">{{weather.name}} ,{{weather.sys.country}}</label><br>
                    <label class="Date" for="Date">{{dataBuilder()}}</label>
                </div>
            </div>

            <div class="Weather-box">
                <div class="temp">{{Math.round(weather.main.temp)}}°C</div><br><br>
                <div class="weather">{{weather.weather[0].main}}</div>
            </div>
        </div>
    </div>
</template>



<style>
.Search-box{
    padding:5px;
    text-align: center;
}
.Search-box .Search{
    display: inline-block;
    font-size: 20px;
    min-width: 97%;
    border:none;
    outline: none;
    padding: 8px;
    appearance: none;
    border-radius: 6px 0px 8px 0px;
    background-color: rgba(255,255,255,0.25);
}
.Search-box .Search:focus{
    border:none;
    border-radius: 0px 6px 0px 8px;
    background-color: rgba(255,255,255,0.50);
}
.main{
  background-image: linear-gradient(to bottom,rgba(0,0,0,0.25),rgba(0,0,0,0.75));
  background-size: cover;
  min-height:100vh;    
}
.location-box{
        text-align: center;
        padding:50px;
}
.location-box .country{
    color:white;
    font-size: 40px;
    font-weight: 300;
}
.location-box .Date{
    color:white;
    font-size: 25px;
    font-weight: 100;
}
.Weather-box{
    text-align: center;
}
.Weather-box .temp
{
    display: inline-flex;
    font-size: 102px;
    color: white;
    background-color: rgba(255,255,255,0.25);
    text-shadow: 3px 6px rgba(255,255,255,0.25);
    border-radius: 16px;
    box-shadow: 3px 6px rgba(0,0,0,0.50);
}
.Weather-box .weather
{

    font-size: 62px;
    font-style: italic;
    color: white;
    text-shadow: 3px 6px rgba(255,255,255,0.25);
    border-radius: 16px;

}



</style>

<script>
export default {
    data(){
     return{
    api_key:'3fb4914726a1b907bd7716457ee7d5fa',
    base_url: 'http://api.openweathermap.org/data/2.5/',
    query:'',
    weather:{}
    }
  },
   methods:{
       fetchweather(e){
           if(e.key == 'Enter')
           {
               fetch(`${this.base_url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
                    .then(res => {
                        return res.json();
                    }).then(this.setResults);
           }
       },
       setResults(results)
       {
           this.weather = results;
       },
       dataBuilder() {
           let d = new Date();
           let months = ["january","February","March","April","May","June","July","August","September","October","November","December"];
           let days = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"]; 


           let day = days[d.getDay()];
           let date = d.getDate();
           let month = months[d.getMonth()];
           let year = d.getFullYear();

           return(`${day} ${date} ${month} ${year} `);
       }
   }
}
</script>