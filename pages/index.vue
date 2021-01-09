<template>
  <div class="container mx-auto mt-24 min-h-screen">
    <h1 class="text-center text-3xl font-bold">Search for a movie</h1>
    <Search v-model="searchParam" @Search="onSearch" />
    <div class=" mx-auto py-8 w-full">
      <h2 v-if="errorMsg.error" class="text-center text-xl font-light text-red-500">{{ errorMsg.msg }}</h2>

      <h2 v-if="results.total > 0" class="text-center text-xl font-light text-green-500 mb-8">Total results : {{ results.total }}</h2>

      <div class="flex flex-row justify-left flex-wrap">
        <Poster v-for="(item, index) in results.list" :key="index" :data="item" />
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

</style>
