<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div class="card">
      <ul class="list-group list-group-flush">
        <li class="list-group-item">Name: <input type="text" v-model="newKittenParams.name"></li>
        <li class="list-group-item">Age: <input type="text" v-model="newKittenParams.age"></li>
        <li class="list-group-item">Image: <input type="text" v-model="newKittenParams.image"></li>
      </ul>
    </div>
    <!-- <p>Name: <input type="text" v-model="newKittenParams.name"></p>
    <p>Age: <input type="text" v-model="newKittenParams.age"></p>
    <p>Image: <input type="text" v-model="newKittenParams.image"></p>
    <button v-on:click="createFunction()">Add</button> -->
    <br>
    <router-link to="/kittens">Back</router-link>
  </div>
</template>

<style>
  .card {
    text-align: center;
  }
</style>

<script>
  import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "Add Kitten!",
        newKittenParams: {}
      };
    },
    created: function () {},
    methods: {
      createFunction: function() {
        console.log("in the create function");
        axios 
          .post('/kittens', this.newKittenParams)
          .then(response => {
            console.log(response.data);
            this.$router.push('/kittens')
          })
      }
    },
  };
</script>