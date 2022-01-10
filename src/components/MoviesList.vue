<template>
  <router-link :to="{name: 'detail', params: { id: movie.id }}">
  <div class="p-0 mb-5 bg-white shadow-none">
      <div class="w-full">
        <img class="w-full" :src="'https://www.themoviedb.org/t/p/original/'+movie.poster_path" alt="">
      </div>
      <label class="block px-4 py-1 mx-auto text-lg font-semibold text-white bg-red-700">{{ movie.original_title }}</label>
  </div>
  </router-link>
</template>

<script>
// import axios from "axios";

export default {
 props: ['movie', 'api_key'],  
 components: {
    
  },
  data() {
    return {
    }
  },
  methods: {
    
  }
}

</script>