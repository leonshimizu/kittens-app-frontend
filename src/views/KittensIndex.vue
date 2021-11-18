<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <router-link to="/kittens/new">Add Kitten</router-link>
    <ul>
      <li v-for="kitten in kittens">
        <p>ID: {{ kitten.id }}</p>
        <p>Name: {{ kitten.name }}</p>
        <p>Age: {{ kitten.age }}</p>
        <button v-on:click="showModal(kitten)">Edit Kitten</button>
        <hr>
      </li>
    </ul>
    <dialog id="show-modal">
      <form method="dialog">
        <p>Name: <input type="text" v-model="currentKitten.name"></p>
        <p>Age: <input type="text" v-model="currentKitten.age"></p>
        <button v-on:click="updateFunction()">Update</button>
        <button v-on:click="deleteFunction()">Delete</button>
        <br>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>

<script>
import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "Welcome Kittens!",
        kittens: {},
        currentKitten: {}
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
      },
      showModal: function(theKitten) {
        console.log("in the show modal");
        this.currentKitten = theKitten;
        document.querySelector("#show-modal").showModal();
      },
      updateFunction: function() {
        console.log("in the update function");
        axios 
          .patch(`/kittens/${this.currentKitten.id}`, this.currentKitten)
          .then(response => {
            console.log(response.data);
          })
      },
      deleteFunction: function(){
        console.log("in the delete function");
        var index = this.kittens.indexOf(this.currentKitten);
        this.kittens.splice(index, 1);
        axios
          .delete(`/kittens/${this.currentKitten.id}`)
          .then(response => {
            console.log(response.data);
          })
      }
    },
  };
</script>