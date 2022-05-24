<template>
  <div class="home">
    <h1>SHANES SOCIAL CREDIT SCORE</h1>
    <button v-on:click="getFriends()">Friends</button>
    <h2>{{ friends }}</h2>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      message: "Online",
      friends: [],
    };
  },
  methods: {
    getFriends: function () {
      this.friends.push("Hello");
      console.log("Hello");
    },
  },
};
</script>
