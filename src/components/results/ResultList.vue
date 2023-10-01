<template>
    <div class="flex flex-col items-center">
        <div class="w-[90%] h-auto px-6 pt-12 mx-auto">
            <h1 v-if="isLoading">Loading recipes...</h1>
            <span v-if="noResultMessage == false">
                <h1 v-if="resultMessage">{{ resultMessage }}</h1>
            </span>
        </div>
        
        <div v-if="results" class="cards-row">
            <ResultCard v-for="result in results" :key="result.idMeal" :result="result"/>
        </div>

        <div v-if="noResultMessage" class=" w-5/6 h-80 mb-5 px-6 md:px-0 lg:px-5 py-5 flex flex-col items-center justify-center">
            <i class="bi bi-exclamation-circle text-slate-300 text-[150px]"></i>
            <h1 class="text-2xl md:text-4xl text-center text-slate-400" v-if="resultMessage">{{ resultMessage }}</h1>
        </div>
    </div>
</template>

<script setup>
import axios from 'axios'
import { ref, defineExpose } from 'vue';
import ResultCard from './ResultCard.vue'

const resultMessage = ref('')
const noResultMessage = ref(false)
const isLoading = ref(null)
const results = ref(null)

const startSearch = (keyword) => {
    isLoading.value = true
    resultMessage.value = ''
    axios.get(`https://www.themealdb.com/api/json/v1/1/search.php?s=${keyword}`)
    .then(res => {
        renderResult(res.data.meals, keyword)
        isLoading.value = false
    })
    .catch(err=>{
        console.log(err);
    })
}

const renderResult = (res, keyword) => {
    if(res){
        resultMessage.value = `${res.length} search results "${keyword}"`
        results.value = res
        noResultMessage.value = false
    }else{
        resultMessage.value = `Recipe for "${keyword}" is not found`
        results.value = ''
        noResultMessage.value = true
    }
}

defineExpose({startSearch})
</script>

<style lang="postcss" scoped>
.cards-row{
    @apply grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 w-[90%] max-h-[750px] px-6 md:px-0 lg:px-5 py-5
}
</style>
