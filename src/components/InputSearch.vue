<template>
    <div class="search-container">
        <div class=" grid grid-cols-12 shadow-md rounded-lg">

            <div class="search-icon-container">
                <i class="las la-2x la-search mx-auto"></i>
            </div>
            <input type="text" v-model="keyword" class="search-input" placeholder="What are you going to cook today?">    
            <button type="submit" class="search-btn" @click="clickSearch">
                <span class="hidden md:block">Search</span>
                <i class="las la-2x la-search mx-auto block md:hidden"></i>
            </button>
        
        </div>
        
        <div class="recommended-tags-container">

            <p class=" text-gray-600">Recommendation : </p>
            <select class="ml-5 border-transparent border-b-2 border-b-amber-400" v-model="selected">
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
.search-container{
    @apply md:mx-16 mx-auto p-10 h-40 w-4/5 md:w-3/4 bg-white relative rounded-lg -mt-16 shadow-lg
}
.search-icon-container{
    @apply bg-slate-100 col-span-1 md:flex items-center content-center rounded-l-lg hidden
}
.search-input{
    @apply w-full my-auto h-12 bg-slate-100 px-5 md:col-span-9 col-span-10 rounded-l-lg md:rounded-none
}
.search-btn{
    @apply bg-amber-500 hover:bg-amber-400 transition col-span-2 rounded-r-lg focus:ring-2
}

.recommended-tags-container{
    @apply flex my-6 mx-5 text-lg flex-row items-center
}
.searchTag {
    @apply bg-amber-500  py-1 px-2 sm:px-5 w-fit  rounded-xl hover:bg-amber-600 hover:text-white transition cursor-pointer focus:ring-2  ring-offset-current ring-offset-2
}
</style>