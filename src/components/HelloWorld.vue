<template>
  <v-main>
    <v-text-field
      v-model="movieSearch"
      class="mx-4"
      label="Search Movie Posters"
    ></v-text-field>
    <v-container fluid>
      <v-row dense>
        <v-col
          v-for="movie in movies[0]"
          :key="movie.id"
          :cols="3"
        >
          <v-card>
            <v-img
              :src="`https://image.tmdb.org/t/p/original${movie.poster_path}`"
              class="white--text align-end"
              gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
              height="80vh"
            >
              <v-card-title v-text="movie.title"></v-card-title>
            </v-img>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>
import axios from "axios";

  export default {
    name: 'HelloWorld',

    data: () => ({
      movieSearch: "",
      movies: [],
      
    }),
    
    watch: {  
      movieSearch(newSearch){
        console.log(process.env.VUE_APP_API_KEY)
        this.movies = [],
        axios
        .get(`https://api.themoviedb.org/3/search/movie?api_key=${process.env.VUE_APP_APIKEY}&language=en-US&query=${newSearch}`)
        .then(res => {   
          this.movies.push(res.data.results)
        });
      }    
        
      
    }
  }
</script>
