<style scoped>

</style>

<template>

<div>
  <h1>Welcome to movies!</h1>
  <input type="text" placeholder="Search by movie name"/>
  <div style="width: 100px" v-for="movie in movies" :key="movie.id">
    {{movie.title}}
  </div>
</div>

</template>

<script>

import axios from 'axios'

export default {
    name: 'home',
    mounted() {
        axios({
          method: "GET",
          "url": "assets/json/movies.json"
        }).then(response => {
          this.movies = JSON.parse(JSON.stringify(response.data));
        }, error => {
          // eslint-disable-next-line
          console.error(error);
        });
    },
    data() {
        return {
          movies:[]
        }
    },
    components: {},
    methods: {}
}

</script>
