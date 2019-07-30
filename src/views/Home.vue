<template>
  <v-container grid-list-xs>
    <v-card class="mx-auto" v-if="weatherData" color="#F9F9F9" max-width="400">
      <v-list-item two-line>
        <v-list-item-content>
          <v-list-item-title class="headline">{{
            weatherData.name
          }}</v-list-item-title>
          <v-list-item-subtitle
            >Mon, 12:30 PM, Mostly sunny</v-list-item-subtitle
          >
        </v-list-item-content>
      </v-list-item>

      <v-card-text>
        <v-layout align-center>
          <v-flex xs6 display-3>
            {{ weatherData.main.temp.toFixed() }}&deg;C
          </v-flex>
          <v-flex xs6>
            <v-img
              src="http://cdn.vuetifyjs.com/images/cards/sun.png"
              alt="Sunny image"
              width="92"
            ></v-img>
          </v-flex>
        </v-layout>
      </v-card-text>

      <v-list-item>
        <v-list-item-icon>
          <v-icon>mdi-send</v-icon>
        </v-list-item-icon>
        <v-list-item-subtitle
          >{{ weatherData.wind.speed }} km/h</v-list-item-subtitle
        >
      </v-list-item>

      <v-list-item>
        <v-list-item-icon>
          <v-icon>mdi-cloud-download</v-icon>
        </v-list-item-icon>
        <v-list-item-subtitle>48%</v-list-item-subtitle>
      </v-list-item>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue, Watch, Prop } from "vue-property-decorator";
import HelloWorld from "../components/HelloWorld.vue";
import Axios from "axios";

// I will take this out and put it in a vuex store
interface Weather {
  base: string;
  clouds: { all: number };
  cod: number;
  coord: { lon: number; lat: number };
  dt: number;
  id: number;
  main: {
    temp: number;
    pressure: number;
    humidity: number;
    temp_min: number;
    temp_max: number;
  };
  name: string;
  sys: {
    type: number;
    id: number;
    message: number;
    country: string;
    sunrise: number;
    sunset: number;
  };
  timezone: number;
  visibility: number;
  weather: [{ id: number; main: string; description: string; icon: string }];
  wind: { speed: string; deg: string };
}

@Component
export default class Home extends Vue {
  // This will be a state member
  private weatherData: Weather = {} as Weather;
  async mounted() {
    // This would live in the vuex store actions
    const response = await Axios.get(
      "https://community-open-weather-map.p.rapidapi.com/weather",
      {
        params: { q: "Cape Town", units: "metric" },
        headers: {
          "X-RapidAPI-Host": "community-open-weather-map.p.rapidapi.com",
          "X-RapidAPI-Key": process.env.VUE_APP_API_KEY
        }
      }
    );
    this.weatherData = response.data;
  }
}
</script>
