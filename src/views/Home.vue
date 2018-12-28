<template>
<div id="app">
<div class="hero" data-bg-image="images/banner.png">
  <div class="container">
    <form v-on:submit.prevent="onSubmit" class="find-location">
      <input type="text" placeholder="Please Enter the City Name and Click on Find Button." v-model="searchTerm">
      <input type="button" @click=getTemps() value="Find">
</form>
  </div>
</div>
<div class="forecast-table" v-if="code === 200">
  <div class="container">
    <div class="forecast-container">
      <div class="today forecast">
        <div class="forecast-header">
        <div class="day"></div>
        </div> <!-- .forecast-header -->
        <div class="forecast-content">
          <div class="location">{{city}}</div>
          <div class="degree">
            <div class="num">{{temps}}<sup>o</sup>C</div>
            <div class="forecast-icon">
              <img src="images/icons/icon-1.svg" alt="" width=90>
            </div>
          </div>
          <span><img src="images/icon-compass.png" alt="">Wind Speed: {{wind}}</span>
        </div>
      </div>
    </div>
  </div>
</div>
<div class="forecast-table" v-if="code === 404">
  <div class="container">
    <div class="forecast-container">
      <div class="today forecast">
        <div class="forecast-header">
        <div class="day"></div>
        </div> <!-- .forecast-header -->
        <div class="forecast-content">
          <div class="location">City Not Found</div>
          <div class="degree">
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
<HelloWorld />
<footer class="site-footer">
  <div class="container">
    <div class="row">
      <div class="col-md-8">
        <form action="#" class="subscribe-form">
          <input type="text" placeholder="Enter your email to subscribe...">
          <input type="button" value="Subscribe">
        </form>
      </div>
      <div class="col-md-3 col-md-offset-1">
        <div class="social-links">
          <a href="#"><i class="fa fa-facebook"></i></a>
          <a href="#"><i class="fa fa-twitter"></i></a>
          <a href="#"><i class="fa fa-google-plus"></i></a>
          <a href="#"><i class="fa fa-pinterest"></i></a>
        </div>
      </div>
    </div>

    <p class="colophon">Copyright 2018 All rights reserved</p>
  </div>
</footer> <!-- .site-footer -->
</div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import Footer from "@/components/Footer.vue";
export default {
  name: "App",
  components: {
    HelloWorld,
    Footer
  }
};
</script>

<script>
import axios from "axios";

export default {
  data() {
    return {
      searchTerm: "",
      temps: [],
      city: [],
      wind: [],
      string: [],
      code: []
          };
  },
  methods: {
    getTemps() {
      let apiKey = "e6ddb341b37bcb705e4a569c80c7596c";
      let searchEndPoint = "https://api.openweathermap.org/data/2.5/weather"; //API URL
      let url = `${searchEndPoint}?q=${this.searchTerm}&units=metric&appid=${apiKey}`;
      axios.get(url).then(response => {
      console.log(response);
      this.string = response.data.name;
      this.temps = response.data.main.temp;
      this.city = response.data.name;
      this.wind = response.data.wind.deg;
      this.code = response.data.cod;
  })
  .catch(error => {
      console.log(error);
      this.code = 404;
  });
    }
  }
};
</script>

<style>
.forecast-table {
  margin-top: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
