<template>
    <section class="overflow-hidden text-gray-700 bg-white body-font">
      <router-link to="/">
        <button class="float-left pt-3 pl-3 font-bold"><i class="fa fa-chevron-left"></i> Back</button>
      </router-link>
  <div class="container px-10 py-10">
    <div class="flex flex-wrap mx-auto">
        <div class="w-full mt-6 lg:w-1/4 lg:pl-10 lg:py-6 lg:mt-0">
            <img :src="'https://www.themoviedb.org/t/p/original/'+movie_detail.poster_path" alt="" class="object-cover object-center w-full border border-gray-200">
        </div>
      
      <div class="w-full mt-6 lg:w-1/2 lg:pl-10 lg:py-6 lg:mt-0">
        <!-- <h2 class="text-sm tracking-widest text-gray-500 title-font">BRAND NAME</h2> -->
        <h1 class="mb-1 text-3xl font-medium text-left text-gray-900 title-font">
            {{ movie_detail.original_title }}
        </h1>
        <div class="flex mb-4">
          <span class="flex items-center">
            <span v-for="(genre,index) in  movie_detail.genres" :key="index" :genre="genre" class="ml-3 text-gray-600">
                {{ genre.name }}
            </span>
          </span>
          
        </div>
        <div class="mb-3">
            <p class="leading-relaxed text-left">{{ movie_detail.tagline }}</p>
        </div>
        <div>
            <p class="mb-1 text-xl font-bold text-left">Overview</p>
            <p class="leading-relaxed text-left">
                {{ movie_detail.overview }}
            </p>
        </div>
      </div>
    </div>
  </div>
</section>
</template>

<script>

export default {

  props: ['movie_detail'],

}
</script>