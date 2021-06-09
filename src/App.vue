<template>
  <div class="w-64 h-auto pt-4 bg-gray-200">
    <div
      id="app"
      :class="
        typeof weather.main != 'undefined' && weather.main.temp_max > 16
          ? 'warm'
          : ''
      "
    >
      <main>
        <div>
          <div class="h-4 w-6 text-black font-sans justify-items-center ml-4 mr-4">
           <i class="fa fa-search text-gray-400 z-20 hover:text-gray-500"></i>
            <input
              type="text"
              class="h-8 w-96 pl-10 pr-20 rounded-lg z-0 focus:shadow focus:outline-none"
              placeholder="Search..."
              v-model="query"
              @keypress="fetchWeather"
            />
          </div>
        </div>
        <div class="pt-6">
          <img src="/map.jpg" alt />
        </div>
        <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
          <div class="bg-gray-200 pt-2 ml-4 w-64">
            <h1
              class="text-black text-xl text-bold pt-2 ml-1 font-ubuntu"
            >{{ weather.name }}, {{ weather.sys.country }}</h1>
            <h2 class="text-black-500 text-xs ml-1 font-ubuntu">Weather forecast.</h2>
            <h3 class="text-black-500 text-xs ml-1 font-ubuntu">Today, {{ dateBuilder() }}</h3>
          </div>
          <div class="text-xs ml-4 flex flex-row pt-4 bg-gray-200">
            <div class="bg-white pt-2 rounded-md">
              <h1 class="text-black font-roboto ml-4 p-2">Temperature</h1>
              <div class="pt-2 h-5 w-6 flex-auto flex space-x-3">
                <div class="flex-auto flex-items-center">
                  <h2
                    class="text-blue-600 text-xl p-2 font-bold"
                  >{{ Math.round(weather.main.temp_max) }}°c</h2>
                  <p class="text-black p-2 font-normal">Maximum</p>
                </div>
                <div class="flex-auto flex-items-center">
                  <h3
                    class="text-blue-600 text-xl p-2 font-bold"
                  >{{ Math.round(weather.main.temp_min) }}°c</h3>
                  <p class="text-black p-2 font-normal">Minimum</p>
                </div>
              </div>
            </div>
            <div class="bg-white text-xs ml-10 pt-2 flex flex-col h-100 rounded-md">
              <h1 class="text-black font-roboto p-2 ml-4 mr-4">Additional Parameters</h1>
              <div class="flex flex-col">
                <div class="text-blue p-2 text-xs">Wind {{ Math.round(weather.main.wind_deg) }}</div>
                <div
                  class="text-blue p-2 text-xs"
                >Pressure {{ Math.round(weather.main.pressure) }}Pa</div>
                <div
                  class="text-blue text-xs p-2 flex flex-row"
                >Precipitation {{ Math.round(weather.main.precipitation) }}</div>
              </div>
            </div>
          </div>
          <div class="bg-gray-200 pt-4 w-100">
            <div class="flex flex-row ml-4 rounded-md bg-white">
              <div class="text-black p-2">
                <p class="text-black text-xs font-Roboto ml-2">Tuesday</p>
                <img src="/sun.png" alt class="h-12" />
                <p class="text-black font-light text-xs w-24 ml-2">Sunny Interval</p>
              </div>
              <div class="text-black p-2 ml-4">
                <p class="text-black text-xs font-Roboto">Wednesday</p>
                <img src="/cloud.png" alt class="h-12" />
                <p class="text-black font-light text-xs w-24">Sunny Interval</p>
              </div>
              <div class="text-black p-2 ml-6 mr-2">
                <p class="text-black text-xs font-Roboto">Thursday</p>
                <img src="/rain.jpg" alt class="h-12" />
                <p class="text-black font-light text-xs w-24">Heavy Rain.</p>
              </div>
            </div>
          </div>
          <div class="bg-gray-200 h-64"></div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      api_key: "c1b5b8e0f2d3cd1fc439e2dbe8118e41",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>


