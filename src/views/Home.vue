<template>
  <div div class="home">
    <nav class="relative flex flex-wrap items-center justify-between px-2 py-3 mb-3 bg-gray-900">
    <div class="container flex flex-wrap items-center justify-between px-4 mx-auto">
      <div class="relative flex justify-between w-full px-4 lg:w-auto lg:static lg:block lg:justify-start">
        <a class="inline-block py-2 mr-4 text-2xl font-bold leading-relaxed text-white whitespace-nowrap" href="/">
          Movies
        </a>
        <button class="block px-3 py-1 text-xl leading-none text-white bg-transparent border border-transparent border-solid rounded outline-none cursor-pointer lg:hidden focus:outline-none" type="button" v-on:click="toggleNavbar()">
          <i class="fa fa-bars"></i>
        </button>
      </div>
      <div v-bind:class="{'hidden': !showMenu, 'flex': showMenu}" class="items-center lg:flex lg:flex-grow">
        <div class="pt-0">
          <input @keyup.enter="searchMovie(search)" v-model="search" type="text" placeholder="Search" class="relative w-full px-3 py-2 text-sm bg-white border-0 rounded-full shadow outline-none placeholder-blueGray-300 text-blueGray-600 focus:outline-none focus:ring"/>
        </div>
      </div>
    </div>
  </nav>
   </div>

  <div v-if="moviesList.length > 0" class="container w-full py-20 mx-auto md:px-40">
      <div class="px-10 mx-auto space-y-6 md:grid lg:grid-cols-3 md:grid-cols-2 mlg:grid-cols-3 md:gap-10 md:space-y-0 md:px-0">
        <MoviesList v-for="(movie,index) in  moviesList" :key="index" :movie="movie" :api_key="api_key"/>
      </div>
      <div class="pl-5 pr-5">
        <button v-if="search === ''" @click="loadMore()" class="w-full p-5 font-bold text-white uppercase bg-blue-700">
        Load More
      </button>
      </div>
  </div>
  
</template>

<script>
import MoviesList from '../components/MoviesList.vue';
import axios from "axios";

export default {

  components: {
    MoviesList, 
  },
  data(){
    return{
        showMenu: false,
        search: '',
        api_key: '9ad1cbfe587962970c9f379c71fef881',
        moviesList: [],
        page: 1,
    }
  },
  methods:{
    toggleNavbar: function(){
      this.showMenu = !this.showMenu;
    },
    async searchMovie(text){
        await axios.get('https://api.themoviedb.org/3/search/movie?api_key='+this.api_key+'&query='+text)
        .then((response) => {
            this.moviesList =  response.data.results;     
        })
        .catch(error => {
            console.log(error.response.data.status_message);
        })
    },
    async getMovies(){
        await axios.get('https://api.themoviedb.org/3/movie/popular?api_key='+this.api_key+'&language=en-US&page='+this.page)
        .then((response) => {
            this.moviesList =  this.moviesList.concat(response.data.results);
        })
        .catch(error => {
            console.log(error.response.data.status_message);
        })
    },
    loadMore: function(){
      this.page = this.page + 1;
      this.getMovies();
    },
  },
  created(){
      this.getMovies();
  }
}
</script>