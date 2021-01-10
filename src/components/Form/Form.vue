<template>
  <form class="form" @submit.prevent="search('SUBMIT')">
    <input
      spellcheck="false"
      type="text"
      placeholder="eg. East London, ZA"
      class="form__input"
      v-model.trim="query"
      @keydown="search"
    />
  </form>
</template>

<script>
import baseURL from "../../data/endpoint";
import API_KEY from "../../data/keys";
export default {
  name: "Form",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    search(event) {
      if (event.key === "Enter" || event.key === "SUBMIT") {
        // get the query
        const query_tokens = String(this.query).split(",");
        if (query_tokens.length === 1) {
          fetch(
            `${baseURL}weather?q=${query_tokens[0]}&units=metric&appid=${API_KEY}`
          )
            .then((res) => {
              return res.json();
            })
            .then((data) => {
              this.$emit("data", data);
            });
        } else if (query_tokens.length == 2) {
          fetch(
            `${baseURL}weather?q=${query_tokens[0]},${query_tokens[1]}&units=metric&appid=${API_KEY}`
          )
            .then((res) => {
              return res.json();
            })
            .then((data) => {
              this.$emit("data", data);
            });
        } else {
          fetch(
            `${baseURL}weather?q=${query_tokens[0]},${query_tokens[1]},${query_tokens[2]}&units=metric&appid=${API_KEY}`
          )
            .then((res) => {
              return res.json();
            })
            .then((data) => {
              this.$emit("data", data);
            });
        }
        return (this.query = "");
      }
    },
  },
};
</script>

<style scoped>
.form {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  background-color: black;
  max-width: 500px;
  margin: 10px auto;
  color: white;
  display: flex;
  opacity: 0.6;
}
.form__input {
  padding: 8px 10px;
  border: none;
  outline: none;
  flex: 1;
  border-radius: 5px 0px 5px 0px;
  text-align: center !important;
  caret-color: blue;
  font-size: 20px;
  font-weight: 600;
}
.form__input:focus {
  border-radius: 0px 5px 0px 5px;
}
</style>
