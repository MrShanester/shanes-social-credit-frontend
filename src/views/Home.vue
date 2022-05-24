<template>
  <div class="home">
    <h1>SHANES SOCIAL CREDIT SCORE</h1>
    <button v-on:click="getFriends()">Friends</button>
    <h2>{{ friends }}</h2>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Online",
      friends: [],
    };
  },
  methods: {
    getFriends: function () {
      axios.get("http://localhost:3000/friend").then((response) => {
        this.friends = response.data;
        console.log(response.data);
      });
    },
  },
};
</script>
