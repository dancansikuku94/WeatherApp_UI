<template>
  <div
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''
    "
  >
    <main>
      <div>
        <div
          class="
            h-4
            w-9
            text-black
            font-sans
            bg-white
            justify-items-center
            pt-6
            ml-5
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
        <div class="bg-white pt-2">
          <h1 class="text-black text-xl text-bold pt-4 ml-5 font-ubuntu">
            {{ weather.name }}, {{ weather.sys.country }}
          </h1>
          <h2 class="text-black-500 text-xs ml-5 font-ubuntu">
            Weather forecast.
          </h2>
          <h3 class="text-black-500 text-sm ml-5 font-ubuntu">
            Today, {{ dateBuilder() }}
          </h3>
        </div>
        <div class="flex flex-row bg-white w-10">
          <div class="bg-white pt-4 rounded-md">
            <h1 class="text-black font-medium justify-items-center ml-10">
              Temperature.
            </h1>
            <div class="pt-6 h-5 w-4 flex-auto flex space-x-3">
              <div class="flex-auto flex-items-center">
                <h2 class="text-blue-600 font-bold">
                  {{ Math.round(weather.main.temp_max) }}°c
                </h2>
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
          <div class="font-medium ml-10 pt-4 rounded-md">
            <h1 class="text-black font-roboto align-center">
              Additional Parameters
            </h1>
            <p class="text-blue font-normal">
              Wind {{ Math.round(weather.main.wind_deg) }}
            </p>
            <p class="text-blue font-normal">
              pressure {{ Math.round(weather.main.pressure) }}Pa
            </p>
            <p class="text-blue font-normal">
              Precipitation{{ Math.round(weather.main.precipitation) }}
            </p>
          </div>
        </div>
        <div class="flex flex-row bg-gray-50 pt-4 h-4 w-10">
          <div class="text-black">
            <p class="text-black font-normal">Tuesday</p>
            <img src="/sun.png" alt="" class="w=4/12 h=1/60" />
            <p class="text-black font-light">{{ weather.main.icons }}</p>
          </div>
          <div class="text-black ml-10">
            <p class="text-black font-normal">Wednesday</p>
            <img src="/cloud.png" alt="" class="w-4/12 h-6/12" />
            <p class="text-black font-light">Sunny Interval.</p>
          </div>
          <div class="text-black ml-10">
            <p class="text-black font-normal">Thursday</p>
            <img src="/rain.jpg" alt="" class="w-4/12 h-6/12" />
            <p class="text-black font-light">Heavy Rain.</p>
          </div>
        </div>
      </div>
    </main>
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


