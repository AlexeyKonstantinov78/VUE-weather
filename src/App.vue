<template>
  <div class="weather" :class="weatherClass">
    <div class="container">
      <div class="card weather-form">
        <input
          class="weather-form__input"
          type="text"
          placeholder="Enter city"
          v-model="searchQuery"
          @keyup.enter="weatherSearch" />
        <button class="weather-form__btn" @click="weatherSearch">Search</button>
      </div>

      <div class="card weather-load" v-if="loading">Loading...</div>
      <div class="card weather-load" v-if="error">
        {{ errorMessages }}
      </div>

      <div
        class="weather-info"
        v-show="
          !error && !loading && location && temperature !== 0 && description
        ">
        <div class="weather-info__text">
          <p class="card">{{ location }}</p>
          <p class="card">{{ temperature }}&#8451;</p>
          <p class="card">{{ description }}</p>
        </div>
      </div>
    </div>

    <div class="weather-bg">
      <div>
        <img
          class="weather-bg__img bg"
          src="./assets/bg.jpg"
          width="100%"
          height="100%"
          alt="Земля" />
        <img
          class="weather-bg__img overcast"
          src="./assets/overcast.avif"
          width="100%"
          height="100%"
          alt="Облачно" />
        <img
          class="weather-bg__img partly-cloudy"
          src="./assets/partly-cloudy.jpg"
          width="100%"
          height="100%"
          alt="почти солнечно" />
        <img
          class="weather-bg__img sunny"
          src="./assets/sunny.webp"
          width="100%"
          height="100%"
          alt="Солнечно" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VUEWeatherApp',

  data() {
    return {
      location: '',
      temperature: 0,
      description: '',
      loading: false,
      error: false,
      errorMessages: '',
      searchQuery: '',
    };
  },
  computed: {
    weatherClass() {
      if (this.description.includes('Sunny')) {
        return 'sunny';
      } else if (this.description.includes('Overcast')) {
        return 'overcast';
      } else if (this.description.includes('Partly cloudy')) {
        return 'partly-cloudy';
      } else {
        return '';
      }
    },
  },

  methods: {
    weatherSearch() {
      const baseUrl = 'http://api.weatherapi.com/v1';
      const KEY = '5477626a1047400b8df101616243004';
      this.loading = true;
      this.error = false;
      // const url = `${baseUrl}/current.json?key=${KEY}&q=${this.searchQuery}&lang=ru`;
      const url = `${baseUrl}/current.json?key=${KEY}&q=${this.searchQuery}`;

      fetch(url)
        .then((response) => response.json())
        .then((data) => {
          if (data.error) {
            throw new Error(data.error.message);
          }
          this.loading = false;
          this.location = data.location.name;
          this.temperature = data.current.temp_c;
          this.description = data.current.condition.text;
          this.resetSearchQuery();
        })
        .catch((error) => {
          this.loading = false;
          this.error = true;
          this.errorMessages = error;
        });
    },
    resetSearchQuery() {
      this.searchQuery = '';
    },
  },
};
</script>
