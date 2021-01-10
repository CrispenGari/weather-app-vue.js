<template>
  <div :class="`app ${hot && 'app__hot'}`">
    <div class="app__main">
      <Header />
      <div class="app__main__main">
        <Form @data="getData" />
        <Weather :data="data" />
      </div>
    </div>
  </div>
</template>

<script>
import { Header, Form, Weather } from "./components";
import baseURL from "./data/endpoint";
import API_KEY from "./data/keys";
export default {
  name: "App",
  components: {
    Header,
    Weather,
    Form,
  },
  data() {
    return {
      data: {},
    };
  },
  methods: {
    getData(data) {
      this.data = data;
    },
  },
  computed: {
    hot() {
      if (Object.keys(this.data).length > 0) {
        return this.data?.main?.temp < 20;
      } else {
        return false;
      }
    },
  },
  mounted() {
    fetch(
      "https://ipfind.co/?ip=196.21.104.1&auth=7b98da30-ff64-4429-ae6a-10d87d82ed4e"
    )
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        const { longitude, latitude } = data;
        fetch(
          `${baseURL}weather?lat=${latitude}&lon=${longitude}&units=metric&appid=${API_KEY}`
        )
          .then((res) => {
            return res.json();
          })
          .then((data) => {
            this.data = data;
          });
      });
  },
};
</script>

<style scoped>
.app {
  width: 100vw;
  height: 100vh;
  overflow-x: hidden;
  overflow-y: scroll;
  background: url(./assets/cold.jpg);
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
.false {
  background: url(./assets/hot.jpg);
}
.app::-webkit-scrollbar {
  display: none !important;
}
.app__main {
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
}
.app__main__main {
  width: 100%;
  padding: 20px;
  display: grid;
  place-items: center;
  flex: 1;
}
</style>
