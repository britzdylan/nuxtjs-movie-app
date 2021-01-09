<template>
  <div class="container mx-auto py-16">
    <h1 class="text-3xl font-bold text-green-500">Title: {{movie.Title}}</h1>
          <img :src="movie.Poster != 'N/A' ? movie.Poster : 'https://via.placeholder.com/300x420.jpg?text=No+poster+available'"  height="100%" :alt="movie.Title"/>
    <ul id="v-for-object" class="demo">
      <li v-for="(value, name) in movie" :key="value" class="text-lg font-medium my-6" >
        <span class="text-grey-800" v-if="name != 'Ratings' && name != 'Poster' && name != 'Response'">{{ name }}:</span> <span v-if="name != 'Response' && name != 'Ratings' && name != 'Poster'" class="text-green-500">{{ value }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movie : {},
      errorMsg : ''
    }
  },
  //  async asyncData({ $http, $get, route }) {
  //     // const data = await $http.$get(`http://www.omdbapi.com/?i=${this.$route.query.i}&apikey=c791c273`)
  //     // return { data }
  //       console.log(route);
  //   }
  async fetch() {
      const data = await fetch(`http://www.omdbapi.com/?i=${this.$route.query.i}&apikey=c791c273`)
      .then(res => res.json())
      if (data.Response == 'False') {
        this.errorMsg = "Oops Something went wrong"
      } else {
        this.movie = data
        console.log(this.movie.keys());
      }
  },
  fetchOnServer : false
}
</script>

<style>

</style>
