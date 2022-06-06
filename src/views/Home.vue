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

    <!-- Button trigger modal -->
    <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#staticBackdrop">
      Add New Associate
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      id="staticBackdrop"
      data-bs-backdrop="static"
      data-bs-keyboard="false"
      tabindex="-1"
      aria-labelledby="staticBackdropLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="staticBackdropLabel">Be Precise, Be Accurate, Be Safe</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <h1>Input Associate Information</h1>
            <br />
            <h2>Name:</h2>
            <input type="text" v-model="newFriendParams.name" />
            <br />
            <p></p>
            <h2>Description:</h2>
            <input type="text" v-model="newFriendParams.description" />
            <br />
            <p></p>
            <h2>Identifying Photo:</h2>
            <input type="text" v-model="newFriendParams.image_url" />
            <br />
            <p></p>
            <h2>Starting Score: 0</h2>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Return</button>
            <button type="button" class="btn btn-primary" v-on:click="this.addFriend()">Create Associate</button>
          </div>
        </div>
      </div>
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
      newFriendParams: {
        score: 0,
        name: "",
        description: "",
        image_url: "",
      },
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
      axios.post("http://localhost:3000/friend", this.newFriendParams).then((response) => {
        this.friends.push(response.data);
        console.log(response.data);
      });
    },
  },
};
</script>
