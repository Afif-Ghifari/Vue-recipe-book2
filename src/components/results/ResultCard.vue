<template>
    <div class="mx-2">
        <div class="card-body">
            <div class="overflow-hidden bg-white border rounded-lg hover:drop-shadow-md">
                <div>
                    <img class="img-card" alt="preview" :src="result.strMealThumb">
                </div>
                <div class="flex flex-col px-6 py-3">
                    <p class="tag">{{ result.strCategory }}</p>
                    <h1 class="my-1">{{ result.strMeal}}</h1>
                    <p class="my-1">Instructions: </p>
                    <p class="my-1 text-justify">{{ result.strInstructions.substring(0, 100)+ '. . .' }}</p>

                    <button class="btn-see-more" @click="toggleModal">Show More</button>
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
.card-body {
    @apply flex flex-col mx-auto my-2 border border-amber-100 max-w-xs md:max-w-[300px] lg:max-w-xs h-auto rounded-lg cursor-pointer shadow-xl hover:shadow-xl hover:shadow-amber-200
}

.img-card {
    @apply object-cover object-center w-full max-h-52
}

.btn-see-more {
    @apply border-y border-amber-500 mb-6 mx-6 my-3 py-2 px-5 font-black transition hover:rounded-lg hover:bg-amber-500 hover:text-white hover:border-amber-500
}

.tag {
    @apply bg-amber-500 text-white py-1 px-2 my-1 sm:px-5 w-fit rounded-xl
}
</style>