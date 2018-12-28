<template>
<div id="app">

<div class="hero" data-bg-image="images/banner.png">
  <div class="container">
    <div class="find-location">
      <input type="text" placeholder="Find your location..." v-model="searchTerm">
      <button  @click=getTemps()>Find</button>
</div>

  </div>
</div>
<div class="forecast-table">
  <div class="container">
    <div class="forecast-container">
      <div class="today forecast">
        <div class="forecast-header">
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
<HelloWorld />
<Footer />
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
      string: []
    };
  },
  methods: {
    getTemps() {
      let apiKey = "e6ddb341b37bcb705e4a569c80c7596c";
      let searchEndPoint = "https://api.openweathermap.org/data/2.5/weather";
      let limit = 5;
      //https://api.openweathermap.org/data/2.5/weather?q=mysore&appid=e6ddb341b37bcb705e4a569c80c7596c
      let url = `${searchEndPoint}?q=${this.searchTerm}&appid=${apiKey}`;

      axios
  .get(url)
  .then(response => {
      console.log(response);
      this.string = response.data.name;
      this.temps = response.data.main.temp;
      this.city = response.data.name;
      this.wind = response.data.wind.deg;

  })
  .catch(error => {
      console.log(error);
  });
    },

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
