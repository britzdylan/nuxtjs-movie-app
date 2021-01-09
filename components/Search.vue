<template>
    <div class="w-2/3 mx-auto flex flex-row mt-4">
        <input 
            v-bind:value="value"
            v-on:input="$emit('input', $event.target.value)" 
            type="text" 
            class="border border-green-300 focus:outline-none focus:border-green-600 focus:none w-full px-2 py-4 rounded-tl-lg rounded-bl-lg outline appearance-none" 
            placeholder="gaurdians of the galaxy" 
        />
        <button @click="$emit('Search')" class="px-8 py-4 bg-green-500 rounded-tr-lg rounded-br-lg text-sm font-medium text-white">Search</button>
    </div>
</template>

<script>

export default {
    name : 'Search',
    emits : ['Search'],
    props: ["value"]
}
</script>

<style>

</style>
