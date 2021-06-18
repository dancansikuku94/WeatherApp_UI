<template>
  <div class="w-100 h-auto pt-4 bg-gray-200">
    <div
      id="app"
      :class="
        typeof weather.main != 'undefined' && weather.main.temp_max > 16
          ? 'warm'
          : ''
      "
    >
      <main>
        <div class="h-4 p-3 w-10 text-black font-sans justify-items-center ml-4 mr-4">
          <!-- <div v-if="field1" class="alert alert-info">
    Current Value: {{field1}}
</div> -->
          <input
            type="text"
            class="h-8 w-96 pl-6 pr-36 rounded-lg focus:shadow focus:outline-none"
            placeholder="Search..."
            v-model="query"
            @keypress="fetchWeather"
          />
        </div>
        <div class="pt-8">
          <div class="h-40 w-100 bg-blue-300">
            <!-- <p class="bg-black l-800 w-100"></p> -->
            <!-- <img src="/map.jpg" alt= /> -->
          </div>
        </div>

        <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
          <div class="bg-gray-200 pt-2 ml-4 w-64">
            <h1
              class="text-black text-xl text-bold pt-2 ml-1 font-ubuntu"
            >{{ weather.name }}, {{ weather.sys.country }}</h1>
            <h2 class="text-black-500 text-xs ml-1 font-ubuntu">Weather forecast.</h2>

            <h3 class="text-black-500 text-xs ml-1 font-ubuntu">Today, {{ dateBuilder() }}</h3>
          </div>
          <div class="text-xs ml-4 mr-4 justify-around flex pt-4 bg-gray-200">
            <div class="bg-white pt-2 p-2 rounded-md">
              <h1 class="text-black font-roboto ml-4 p-2">Temperature</h1>
              <div class="pt-2 h-4 flex-auto flex">
                <div class="flex-auto flex-items-center">
                  <div class="flex">
                    <h2
                      class="text-blue-600 text-4xl pt-0 p-2 font-400"
                    >{{ Math.round(weather.main.temp_max) }}</h2>
                    <h class="text-black font-xs mr-4 mt-4">°c</h>
                  </div>
                  <p class="text-black p-2 font-normal">Maximum</p>
                </div>
                <div class="flex-auto flex-items-center">
                  <div class="flex">
                    <h3
                      class="text-blue-600 text-4xl p-2 pt-0 font-400"
                    >{{ Math.round(weather.main.temp_min) }}</h3>
                    <p class="text-black mr-4 mt-4 font-xs">°c</p>
                  </div>
                  <p class="text-black p-2 font-normal">Minimum</p>
                </div>
              </div>
            </div>
            <div class="bg-white text-xs ml-2 pt-2 flex flex-col h-100 rounded-md">
              <h1 class="text-black font-roboto p-2 ml-4 mr-4">Additional Parameters</h1>

              <div class="flex justify-between p-2">
                <p>Wind</p>
                <p class="text-blue-300">{{ Math.round(weather.main.wind_deg) }}</p>
              </div>

              <div class="flex justify-between text-blue p-2 text-xs">
                <p>Pressure</p>
                <p class="text-blue-300">{{ Math.round(weather.main.pressure) }}Pa</p>
              </div>
              <div class="text-blue text-xs p-2 flex justify-between">
                <p>Precipitation</p>
                <p class="text-blue-300">{{ Math.round(weather.main.precipitation) }}</p>
              </div>
            </div>
          </div>
          <div class="bg-gray-200 pt-4 w-60 mr-4">
            <div class="flex flex-row ml-4 justify-around rounded-md bg-white">
              <div class="text-black p-2">
                <p class="text-black text-xs font-Roboto ml-2">{{ dateBuilder() }}</p>
                <img src="http://openweathermap.org/img/wn/10d@2x.png" alt class="h-20 p-2" />
                <p class="text-black font-light text-xs w-24 pt-0 p-2">Sunny Interval</p>
              </div>
              <div class="text-black p-2 ml-4">
                <p class="text-black text-xs font-Roboto">{{ dateBuilder() }}</p>
                <img src="http://openweathermap.org/img/wn/04d@2x.png" alt class="h-20 p-2" />
                <p class="text-black font-light text-xs p-2 pt-0 w-24">Sunny Interval</p>
              </div>
              <div class="text-black p-2 ml-6 mr-2">
                <p class="text-black text-xs font-Roboto">Thursday</p>
                <img src="http://openweathermap.org/img/wn/11n@2x.png" alt class="h-20 p-2" />
                <p class="text-black font-light text-xs p-2 pt-0 w-24">Heavy Rain.</p>
              </div>
            </div>
          </div>
          <div class="bg-gray-200 h-48"></div>
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
