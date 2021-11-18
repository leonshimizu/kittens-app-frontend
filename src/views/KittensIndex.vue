<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="kitten in kittens">
        <p>ID: {{ kitten.id }}</p>
        <p>Name: {{ kitten.name }}</p>
        <p>Age: {{ kitten.age }}</p>
      </li>
    </ul>
  </div>
</template>

<style></style>

<script>
import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "Welcome Kittens!",
        kittens: {}
      };
    },
    created: function () {
      this.indexFunction();
    },
    methods: {
      indexFunction: function() {
        console.log("in the index function");
        axios
          .get('/kittens')
          .then(response => {
            console.log(response.data);
            this.kittens = response.data;
          })
      }
    },
  };
</script>