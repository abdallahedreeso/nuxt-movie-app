<template>
  <div>
    <v-container>
     <Nuxt-link to="/"><v-btn color="error">
        Go Back
      </v-btn></Nuxt-link>
      <div v-if="isLoading" class="loading">
        <v-progress-circular :size="70" :width="7" color="dark" indeterminate></v-progress-circular>
      </div>
      <div v-else>
        <v-row style="padding:10px 0px;">
          <v-col xl="6" md="6" sm="6" xs="12">
            <v-card>
              <v-img
                id="image"
                height="300"
                :src="`https://image.tmdb.org/t/p/w500/${movies.poster_path}`"
              ></v-img>
            </v-card>
          </v-col>
          <v-col xl="6" md="6" sm="6" xs="12">
            <h3>{{ movies.title }}</h3>
            <h4>
              <span style="text-decoration: underline;">
                <i>Tag Line</i>
              </span>
              {{ movies.tagline }}
            </h4>
            <h4>
              <span style="text-decoration: underline;">
                <i>Realse :</i>
              </span>
              {{ movies.release_date }}
            </h4>
            <h4>
              <span style="text-decoration: underline;">
                <i>Duration :</i>
              </span>
             {{movies.runtime}}
            </h4>
            <p>
              <span style="text-decoration: underline;">
                <i>Overview :</i>
              </span>
             {{movies.overview}}
            </p>
          </v-col>
        </v-row>
      </div>
    </v-container>
  </div>
</template>
<script>
import axios from 'axios'
export default {
   head(){
    return{
      title:this.movies.title,
      meta:[
        {
          charset:'utf-8'
        },
        {
          name:'viewport', content:'width=device-width, height=device-height,initial-scale=1'
        },
        {
          hid:'description',
          name:'description',
          content:'Get all Move App'
        }
      ]
    }
  },
  data() {
    return {
      movies: [],
      isLoading: false
    }
  },
  methods: {
    async getSingleMovies() {
      this.isLoading = true;
      const response = await axios.get(`https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=48ea694f350f86ea6c318b836a2d7a93&language=en-US&page=1`);
      this.movies = response.data;
      this.isLoading = false;
      console.log(this.movies);
    }
  },
  async fetch() {
    await this.getSingleMovies();
  }
}
</script>
<style >
.loading {
  display: flex;
  justify-content: center;
  margin: 50px 0px;
}
</style>
