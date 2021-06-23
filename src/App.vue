<template>
  <div class="w-150 h-auto pt-4 bg-gray-200">
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
          <div
            class="
              h-4
              w-9
              text-black
              font-roboto
              justify-items-center
              pt-3
              ml-1
            "
          >
            <input
              type="text"
              class="search-bar"
              placeholder="Search"
              v-model="query"
              @keypress="fetchWeather"
            />
          </div>
        </div>
        <div class="pt-10">
          <img src="/map.jpg" alt="" />
        </div>
        <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
          <div class="bg-gray-200 pt-2 ml-0">
            <h1 class="text-black text-xl text-bold pt-4 ml-1 font-ubuntu">
              {{ weather.name }}, {{ weather.sys.country }}
            </h1>
            <h2 class="text-black-500 text-xs ml-1 font-ubuntu">
              Weather forecast.
            </h2>
            <h3 class="text-black-500 text-sm ml-1 font-ubuntu">
              Today, {{ dateBuilder() }}
            </h3>
          </div>
          <div class="flex ml-2 bg-gray-200 p-2">
            <div class="bg-white rounded-md p-2">
              <h1 class="text-black font-roboto justify-items-center ml-5">
                Temperature
              </h1>
              <div class="bg-white pt-6 flex-auto flex space-x-3">
                <div class="flex-auto flex-items-center">
                  <h1 class="text-blue-600 font-bold">
                    {{ Math.round(weather.main.temp_max) }}°c
                  </h1>
                  <p class="text-black font-normal">Maximum</p>
                </div>
                <div class="flex-auto flex-items-center">
                  <h3 class="text-blue-600 font-bold">
                    {{ Math.round(weather.main.temp_min) }}°c
                  </h3>
                  <p class="text-black font-normal">Minimum</p>
                </div>
              </div>
            </div>
            <div class="ml-4 h-100 p-3 rounded-md bg-white">
              <h1 class="text-black font-roboto">Additional Parameters</h1>
              <div class="flex-col justify-between p-2">
                <div class="text-blue font-normal flex justify-between p-2">
                  <p>Wind</p>
                  <p class="text-blue-500">
                    {{ Math.round(weather.main.wind_deg) }}
                  </p>
                </div>
                <div class="text-blue font-normal flex justify-between p-2">
                  <p>pressure</p>
                  <p class="text-blue-500">
                    {{ Math.round(weather.main.pressure) }}Pa
                  </p>
                </div>
                <div class="text-blue font-normal flex justify-between p-2">
                  <p>Precipitation</p>
                  <p class="text-blue-500">
                    {{ Math.round(weather.main.precipitation) }}
                  </p>
                </div>
              </div>
            </div>
          </div>
          <div class="bg-gray-200 w-100 pt-2">
            <div class="flex flex-row bg-white justify-between pt-4">
              <div>
                <p class="text-black font-normal p-2">Tuesday</p>
                <img src="/sun.png" alt="" class="h=12" />
                <p class="text-black font-light text-xs">Sunny Interval</p>
              </div>
              <div class="ml-10">
                <p class="text-black p-2 font-normal">Wednesday</p>
                <img src="/cloud.png" alt="" class="h-12" />
                <p class="text-black font-light text-xs">Sunny Interval.</p>
              </div>
              <div class="ml-10">
                <p class="text-black p-2 font-normal">Thursday</p>
                <img src="/rain.jpg" alt="" class="h-12" />
                <p class="text-black font-light text-xs">Heavy Rain.</p>
              </div>
            </div>
          </div>
          <div class="bg-gray-200"></div>
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


