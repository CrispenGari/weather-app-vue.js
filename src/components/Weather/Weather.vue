<template>
  <div class="weather">
    <div class="weather__country" v-if="show">
      {{ city }}
    </div>
    <div class="weather__date__time">
      {{ dateTime }}
    </div>
    <div class="weather__temperature" v-if="show">
      <h1>{{ temperature }}</h1>
      <p>{{ main }}</p>
      <p>{{ description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Weather",
  data() {
    return {};
  },
  props: {
    data: Object,
  },
  computed: {
    show() {
      return Object.keys(this.data).length > 0;
    },
    city() {
      return `${this.data?.name}, ${this?.data?.sys?.country}`;
    },
    temperature() {
      return `${Math.floor(this.data?.main?.temp)}° C`;
    },
    main() {
      if (this.data?.weather) {
        return `${this.data?.weather[0]?.main}`.toLowerCase();
      }
      return "loading..";
    },
    description() {
      if (this.data?.weather) {
        return `${this.data?.weather[0]?.description}`.toLowerCase();
      }
      return "loading..";
    },
    dateTime() {
      const days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Sataday",
      ];
      const months = [
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

      const date = new Date();
      const month = date.getMonth();
      const day = date.getDay();
      const date_ = date.getDate();
      const year = date.getFullYear();
      const hour = date.getHours();
      const minute = date.getMinutes();
      const second = date.getSeconds();

      return `${days[day]}
       ${date_} ${months[month]} ${year},
        ${String(hour).length === 1 ? "0" + hour : hour}:${
        String(minute).length === 1 ? "0" + minute : minute
      }:${String(second).length === 1 ? "0" + second : second}`;
    },
  },
};
</script>

<style scoped>
.weather {
  background: rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  width: 100%;
  max-width: 500px;
  display: grid;
  place-items: center;
  padding: 20px;
  color: white !important;
  height: 100%;
  max-height: 40vh;
  box-shadow: 1px 1px 0 0 rgb(83, 141, 160);
  user-select: none;
  user-zoom: none;
  margin: 20px auto;
}
.weather__country {
  text-align: center;
  font-size: 24px;
  font-weight: 500px;
}
.weather__date__time {
  color: darkgray;
  font-size: 15px;
}
.weather__temperature {
  width: 100%;
  display: grid;
  place-items: center;
}
.weather__temperature > h1 {
  font-size: 60px;
  text-shadow: 3px 3px black !important;
  font-weight: 500;
}
.weather__temperature > p {
  text-align: center;
  margin-top: 5px;
  color: darkgray;
  font-size: 15px;
}
.weather__temperature > p:last-child {
  color: white;
  font-style: italic;
}
</style>
