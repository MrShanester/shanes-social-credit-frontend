<template>
  <div class="home">
    <h1>SHANES SOCIAL CREDIT SCORE</h1>
    <img src="https://t4.ftcdn.net/jpg/02/93/03/75/360_F_293037586_KE5TaXukXeKkHJ2RAbDeqJuUOhf2qav0.jpg" alt="" />
    <br />
    <h2>Always Watching</h2>
    <p></p>
    <h3>"No good deed unnoticed, no bad deed unpunished."</h3>
    <br />

    <div v-for="friend in friends" v-bind:key="friend.id">
      <img v-bind:src="friend.image_url" v-bind:alt="`No Image`" />
      <h2>{{ friend.name }}</h2>
      <h3>{{ friend.description }}</h3>
      <p>Points: {{ friend.score }}</p>
      <router-link v-bind:to="`/friendshow/${friend.id}`">
        <button>View Social Status</button>
      </router-link>
    </div>
    <br />
    <div class="modal">
      <button>Add New Associate</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Online",
      friends: [],
      newFriendParams: {},
    };
  },
  created: function () {
    this.getFriends();
  },
  methods: {
    getFriends: function () {
      axios.get("http://localhost:3000/friend").then((response) => {
        this.friends = response.data;
        console.log(response.data);
      });
    },
    addFriend: function () {
      axios.post("http://localhost:3000/friend" + this.newFriendParams).then((response) => {
        this.friends.push(response.data);
        console.log(response.data);
      });
    },
  },
};
</script>
