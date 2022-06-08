<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 20 ? 'warn' : ''">
      <main>
        <div class="search__box">
          <input type="text" class="search-bar" placeholder="Search.." v-model="query" v-on:keypress="fetchWeather">
        </div>
        <div class="weather__wrap" v-if="typeof weather.main != 'undefined' ">
        <div class="location__box">
          <div class="location">{{weather.name}} , {{weather.sys.country}}</div>
          <div class="date">{{dateBuild()}}</div>
        </div>
        <div class="weather__box">
          <span class="temp">{{Math.round(weather.main.temp)}}</span>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
      </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      api_key: 'e690569dc433c58bfc5542caefee0600',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e){
      if(e.key == "Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json()
        })
        .then(this.setResults)

      }
    },
    setResults(results){
      this.weather = results

    },
    dateBuild(){
      let d = new Date()
      let month = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October ", "November", "December"]
      let days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]
      let day = days[d.getDay()]
      let date = d.getDate()
      let months =  month[d.getMonth()]
      let year = d.getFullYear()

      return ` ${day} ${date} ${months} ${year} `
    }
  }

}
</script>

<style>
 *{
   margin: 0;
   padding: 0;
   box-sizing: border-box;
 }
 body{
   font-family: 'montserrat', sans-serif;
 }
 #app{
   background-image: url('./assets/imgs.jpg');
   background-position: center;
   background-repeat: no-repeat;
   background-size: cover;
   transition: .4s;
 }
 #app.warn{
   background-image: url('./assets/imgs3.jpg');
 }
 main{
   display: grid;
   grid-template-columns: 50% 50%;
   min-height:100vh;
   padding: 25px;
   background-image: linear-gradient(to bottom , rgba(68, 68, 68, 0.25) , rgb(37, 37, 37));
 }
 .search__box{
   width: 90%;
 }
 .search__box .search-bar{
   margin-top: 25vh;
   display: block;
   width: 100%;
   padding: 15px;
   color: #414141;
   font-size: 20px;
   bottom: none;
   outline: none;
   appearance: none;
   background: transparent;
   background-color: rgba(255, 255,255, .5);
   font-size: 20px;
   font-weight: bolder;
   border-radius: 0px 18px 0px 18px;
   box-shadow: 0  0 10px #000;
   transition: .4s;
 }
 .search__box .search-bar:focus{
   box-shadow: 0px 0px 16px rgba(0, 0,0, .25);
   background-color: rgba(255, 255,255, .75);
   border-radius: 16px 0px 16px 0px;
 }

 .location__box .location{
   margin-top: 10vh;
   color: #fff;
   font-size: 32px;
   font-weight: 600px;
   text-align: center;
   text-shadow: 1px 3px rgb(37, 37, 37);
 }

 .location__box .date{
   color: #fff;
   font-size: 20px;
   font-weight: 400px;
   font-style: italic;
   text-align: center;
 }

 .weather__box{
   text-align: center;
 }

 .weather__box .temp{
   display: inline-block;
   padding: 10px 25px;
   color:#fff;
   font-size: 100px;
   font-weight: 900;
   text-shadow: 3px 6px rgb(37, 37, 37);
   background-color: #797979;
   border-radius: 20px;
   margin: 30px 0;
   box-shadow: 3px 6px rgba(0, 0,0, .25);
 }

 .weather__box .weather{
   color: #fff;
   font-size: 28px;
   font-weight: 700;
   font-style: italic;
   text-shadow: 3px 6px rgba(0, 0,0, .25);
 }

</style>