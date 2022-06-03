<template>
  <div>
    <img v-bind:src="friend.image_url" v-bind:alt="`No Image`" />
    <h1>{{ friend.name }}</h1>
    <br />
    <h2>Defining Features: {{ friend.description }}</h2>
    <br />
    <h2>Social Credit Score: {{ friend.score }}</h2>
    <p></p>
    <p></p>

    <br />
    <br />
    <h1>Verifiable Deeds</h1>
    <p>-------------------------------------------</p>
    <div v-for="deed in deeds" v-bind:key="deed.id">
      <h2>{{ deed.deed }}</h2>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Online",
      friend: {},
      deeds: [],
      switch: false,
      button: true,
    };
  },
  created: function () {
    this.getFriends();
    this.getDeeds();
  },
  methods: {
    getFriends: function () {
      axios.get("http://localhost:3000/friend/" + this.$route.params.id).then((response) => {
        this.friend = response.data;
        console.log(response.data);
      });
    },
    getDeeds: function () {
      axios.get("http://localhost:3000/friend/" + this.$route.params.id + "/deeds").then((response) => {
        this.deeds = response.data;
        console.log(response.data);
      });
    },
  },
};
</script>
