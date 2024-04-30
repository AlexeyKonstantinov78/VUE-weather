<template>
  <div class="weather">
    <div class="container">
      <div class="card weather-form">
        <input
          class="weather-form__input"
          type="text"
          placeholder="Enter city" />
        <button class="weather-form__btn">Search</button>
      </div>

      <div class="card weather-load">Loading...</div>

      <div class="weather-info">
        <div class="weather-info__text">
          <p class="card">Phuket</p>
          <p class="card">29&#8451;</p>
          <p class="card">Sunny</p>
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
    return {};
  },

  mounted() {},

  methods: {},
};
</script>
