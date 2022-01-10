<template>

    <MovieDetail :movie_detail="movie_detail"/>
</template>

<script>

import MovieDetail from '../components/MovieDetail.vue';
import axios from "axios";

export default {

  components: {
    MovieDetail,
  },
  props: [],
  data(){
    return{
        api_key: '9ad1cbfe587962970c9f379c71fef881',
        movie_detail: '',
        movie_id: this.$route.params.id,
    }
  },
  methods:{
  async getDetail(){
        await axios.get('https://api.themoviedb.org/3/movie/'+this.movie_id+'?api_key='+this.api_key+'&language=en-US')
        .then((response) => {
            this.movie_detail = response.data;
        })
        .catch(error => {
            console.log(error.response.data.status_message);
        })
    },    
  },
  created(){
      this.getDetail();
  }
}
</script>