<template>
  <div class="dropdown">
    <div v-if="joke == null">
      <button v-on:click="getJoke" class="button">Get a joke</button>
    </div>
    <div v-if="joke != null">
      <button v-on:click="getJoke" class="button">{{ joke.value }}</button>
    </div>
  </div>
  <br />
  <div v-if="joke != null">
    <img
      alt="Chuck Norris is dancing"
      src="../assets/chuck-norris-dancing.gif"
      style="max-width: 50%"
      @mouseover="hover = true"
      @mouseleave="hover = false"
    />
    <div v-if="hover">
      <p>Categories: {{ joke.categories }}</p>
      <p>Created at: {{ joke.createdAt }}</p>
      <p>Image: <img :src="joke.iconUrl" /></p>
      <p>Id: {{ joke.id }}</p>
      <p>Updated at: {{ joke.updatedAt }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";

type Joke = {
  categories: string[]; // ["animal", "dev"]
  createdAt: Date; // "2019-06-02 08:47:39.43184"
  iconUrl: string; // "https://assets.chucknorris.host/img/avatar/chuck-norris.png"
  id: string; // "bwoz2uwsqnwmyawyxdvo1w"
  updatedAt: Date; // "2019-06-02 08:47:39.43184"
  value: string; // "Chuck Norris finished World of Warcraft."
};

export default defineComponent({
  name: "JokeRequest",
  data: () => {
    return {
      joke: null as null | Joke,
      hover: false as boolean,
    };
  },
  methods: {
    getJoke() {
      axios
        .get("https://api.chucknorris.io/jokes/random")
        .then((response) => {
          console.log(response.data);
          let j: Joke = {
            categories: response.data.categories,
            createdAt: new Date(response.data.created_at),
            iconUrl: response.data.icon_url,
            id: response.data.id,
            updatedAt: response.data.updated_at,
            value: response.data.value,
          };
          this.joke = j;
        })
        .catch((error) => console.log(error));
    },
  },
});
</script>

<style scoped>
/* credits: https://www.w3schools.com/css/css_dropdowns.asp */

.button {
  background-color: #29abe2;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
}

.button:hover {
  background-color: #f15a24;
  color: white;
}
</style>
