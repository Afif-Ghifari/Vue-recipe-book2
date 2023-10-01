<template>
    <div class="mx-2">
        <div class="card-container">
            <div class="card-body">
                <div>
                    <img class="card-img" alt="preview" :src="result.strMealThumb">
                </div>
                <div class="card-desc">
                    <div class=" h-3/4">
                        <p class="tag">{{ result.strCategory }}</p>
                        <h1 class="my-1">{{ result.strMeal}}</h1>
                        <p class="my-1">Instructions: </p>
                        <p class="my-1 text-justify">{{ result.strInstructions.substring(0, 100)+ '. . .' }}</p>
                    </div>
                    <div class="h-1/4 px-2">
                        <button class="btn-see-more" @click="toggleModal">Show More</button>
                    </div>
                </div>
            </div>
        </div>
        
        <ResultModal v-if="showModal" :result="result" @toggleModal="toggleModal"></ResultModal>        
    </div>
</template>

<script setup>
import { ref,  defineProps } from 'vue';
import ResultModal from './ResultModal.vue'

const props = defineProps({result: Object})
const showModal = ref(false)

const toggleModal = () => {
    console.log(props);
    showModal.value = !showModal.value
}

</script>

<style lang="postcss" scoped>
.card-container {
    @apply flex flex-col mx-auto min-h-[550px] my-2 border border-amber-100 max-w-xs md:max-w-[300px] lg:max-w-xs 
    rounded-lg cursor-pointer shadow-xl hover:shadow-xl hover:shadow-amber-200
}

.card-body{
    @apply bg-white border border-slate-200 h-full min-h-[550px] rounded-lg hover:drop-shadow-md
}

.card-img {
    @apply object-cover object-center w-full max-h-56 
}
.card-desc{
    @apply flex flex-col justify-between px-2 sm:px-6 py-3 h-full min-h-[325px]
}

.btn-see-more {
    @apply border-y border-amber-500 w-full mb-6 mx-auto my-3  py-2 px-5 font-black transition hover:rounded-lg hover:bg-amber-500 hover:text-white hover:border-amber-500
}

.tag {
    @apply bg-amber-500 text-white py-1 px-2 my-1 sm:px-5 w-fit rounded-xl
}
</style>