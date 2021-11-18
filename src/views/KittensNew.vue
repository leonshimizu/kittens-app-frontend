<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>Name: <input type="text" v-model="newKittenParams.name"></p>
    <p>Age: <input type="text" v-model="newKittenParams.age"></p>
    <button v-on:click="createFunction()">Add</button>
  </div>
</template>

<style></style>

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
          })
      }
    },
  };
</script>