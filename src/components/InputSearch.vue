<template>
    <div class="search-section">
        <div class="search-container">

            <div class="search-icon-container">
                <i class="bi bi-search text-xl mx-auto"></i>
            </div>
            <input type="text" v-model="keyword" class="search-input" placeholder="Let's get cooking!">    
            <button type="submit" class="search-btn" @click="clickSearch">
                <span class="hidden md:block">Search</span>
                <i class="bi bi-search text-xl mx-auto block md:hidden"></i>
            </button>
        
        </div>
        
        <div class="recommended-tags-container">

            <p class=" text-gray-600">Recommendation : </p>
            <select v-model="selected">
                <option v-for="recommendList in recommended" :key="recommendList">{{ recommendList }}</option>
            </select>
        </div>
    </div>
</template>

<script setup>
import { ref, defineEmits, watch } from 'vue';

const recommended = ref(['Rendang', 'Steak', 'Salad', 'Rice'])
const selected = ref('')
const keyword = ref('')

const emits = defineEmits(['startSearch'])
function clickSearch(){
    emits('startSearch', keyword.value)
}

watch(()=>{
        keyword.value = selected.value
})
</script>

<style lang="postcss" scoped>
.search-section{
    @apply md:mx-16 mx-auto py-10 px-1 md:px-10 max-h-44 w-11/12 md:w-3/4 bg-white relative rounded-lg -mt-10 sm:-mt-16 shadow-lg
}
.search-container{
    @apply grid grid-cols-12 shadow-md rounded-lg
}
.search-icon-container{
    @apply bg-slate-100 col-span-1 md:flex items-center content-center rounded-l-lg hidden
}
.search-input{
    @apply w-full my-auto h-12 bg-slate-100 px-1 sm:px-5 col-span-9 sm:col-span-10 md:col-span-9 rounded-l-lg md:rounded-none
}
.search-btn{
    @apply bg-amber-500 hover:bg-amber-400 transition col-span-3 sm:col-span-2 rounded-r-lg focus:ring-2
}

.recommended-tags-container{
    @apply flex my-6 mx-5 text-lg flex-col sm:flex-row items-start
}
.recommended-tags-container select{
    @apply ml-0 md:ml-5 w-36 border-transparent border-b-2 border-b-amber-400
}

.searchTag {
    @apply bg-amber-500  py-1 px-2 sm:px-5 w-fit  rounded-xl hover:bg-amber-600 hover:text-white transition cursor-pointer focus:ring-2  ring-offset-current ring-offset-2
}
</style>