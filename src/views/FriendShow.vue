<template>
  <div>
    <h1>{{ friend.name }}</h1>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Online",
      friend: [],
    };
  },
  created: function () {
    this.getFriends();
  },
  methods: {
    getFriends: function () {
      axios.get("http://localhost:3000/friend/" + this.$route.params.id).then((response) => {
        this.friend = response.data;
        console.log(response.data);
      });
    },
  },
};
</script>
