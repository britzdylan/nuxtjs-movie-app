<template>
    <div  class="w-auto p-0 bg-white rounded mb-4 shadow-lg h-auto overflow-hidden mx-2">
        <NuxtLink :to="{ name: 'movie-slug', params: { slug: data.Title.toLowerCase().replace(/ /g,'-') }, query : { i : data.imdbID } }">
        <div class=" overflow-hidden h-full">
          <img :src="data.Poster != 'N/A' ? data.Poster : 'https://via.placeholder.com/300x420.jpg?text=No+poster+available'"  height="100%" :alt="data.Title"/>
        </div>
        </NuxtLink>
      </div>
</template>

<script>

export default {
    name : 'Poster',
    props : {
        data : {
            type : Object,
            required : true
        }
    }
}
</script>

<style>

</style>
