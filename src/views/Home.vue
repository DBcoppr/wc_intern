<style scoped src="../assets/css/moviepage.css">

</style>

<template>

<main>
  <h1>Welcome to Movies!</h1>
  <input type="text" id="searchbar" v-model="search" placeholder="Search by movie name" />
  <div class="header-btn">
      <button @click="showFavorites = false; showAllMovies = true">All Movies</button>
      <button @click="showFavorites = true; showAllMovies = false">My Favourites</button>
  </div>
  <h2 v-if="showFavorites" class="fav-title">My Favourite Movies</h2>
   <div class="movie-container" >
     <div class="movie"  v-for="movie in filteredMovies" :key="movie.id">
        <img src="../assets/movie-icon.png" alt="movieicon"/>
        <p>{{movie.title}}</p>
        <button class="fav-btn" v-if="showAllMovies" @click="addToFavorites(movie) ">Add to favourite</button>
        <button class="fav-btn" v-if="showFavorites" @click="removeFromFavorites(movie)">Remove Favourite</button>
     </div>
   </div>
</main>

</template>

<script>

import axios from 'axios'

export default {
    name: 'home',
    async mounted() {
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
    computed:{
      filteredMovies:function(){
       if (this.showFavorites) {
        return this.favorites.filter(movie => {
          return movie.title.toLowerCase().includes(this.search.toLowerCase())
        })
      } else {
        return this.movies.filter(movie => {
          return movie.title.toLowerCase().includes(this.search.toLowerCase())
        })
      }
    }
      
    },
    data() {
        return {
          movies:[],
          favorites: [],
          showFavorites: false,
      showAllMovies: true,
          search:""
        }
    },
    components: {},
    methods: {
      addToFavorites(movie) {
      this.favorites.push(movie)
    },
    removeFromFavorites(movie) {
      const index = this.favorites.indexOf(movie)
      if (index > -1) {
        this.favorites.splice(index, 1)
      }
    }
    }
}

</script>
