<template>
  <div class="container mx-auto mt-24 min-h-screen">
    <h1 class="text-center text-3xl font-bold">Search for a movie</h1>
    <div class="w-2/3 mx-auto flex flex-row mt-4">
      <input v-model="searchParam" type="text" class="border border-green-300 focus:outline-none focus:border-green-600 focus:none w-full px-2 py-4 rounded-tl-lg rounded-bl-lg outline appearance-none" placeholder="gaurdians of the galaxy" />
      <button @click="onSearch" class="px-8 py-4 bg-green-500 rounded-tr-lg rounded-br-lg text-sm font-medium text-white">Search</button>
    </div>
    <div class=" mx-auto py-8 w-full">
      <h2 v-if="errorMsg.error" class="text-center text-xl font-light text-red-500">{{ errorMsg.msg }}</h2>

      <h2 v-if="results.total > 0" class="text-center text-xl font-light text-green-500 mb-8">Total results : {{ results.total }}</h2>

      <div class="flex flex-row justify-left flex-wrap">
      <div v-for="(item, index) in results.list" :key="index" class="w-auto p-0 bg-white rounded mb-4 shadow-lg h-auto overflow-hidden mx-2">
        <NuxtLink :to="{ name: 'movie-slug', params: { slug: item.Title.toLowerCase().replace(/ /g,'-') } }">
        <div class=" overflow-hidden h-full">
          <img :src="item.Poster ? item.Poster : ''"  height="100%" :alt="item.Title"/>
        </div>
        </NuxtLink>
      </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchParam : '',
      searchResult : [],
      errorMsg : {
        error : false,
        msg : 'Oops Something went wrong'
      },
      results : {
        total : 0,
        list : {}
      }
    }
  },
  methods : {
    async onSearch() {
      this.errorMsg.error = false;
      let response = await fetch(`http://www.omdbapi.com/?s=${this.searchParam}&apikey=c791c273`)

      if (response.ok) {
        this.searchResult = await response.json()
        if (this.searchResult.Response == "True") {
          this.getData(this.searchResult)
        } else {
          this.errorMsg.error = true
        }
      } else {
        console.log('Error' + response.status);
        this.errorMsg.error = true
      }
    },
    getData(data) { 
      this.results.total = data.totalResults;
      this.results.list = data.Search;
      console.log(this.results.list);
    }
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
