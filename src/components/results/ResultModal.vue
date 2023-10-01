<template>
    <div class="modal-container" @click.self="$emit('toggleModal')">
        <div class="modal">
            <div class="w-1/2" id="image">
                <img class="img-recipe" :src="this.result.strMealThumb">
            </div>
            <div class="modal-body" id="desc">
                <div class="my-2">
                    <h1 class="font-black text-center md:text-left">{{ result.strMeal }}</h1>
                    <p class="tag">{{ result.strCategory }}</p>
                </div>
                <div class="my-2">
                    <h2 class="font-bold">Ingredients: </h2>
                    <ul class="mx-5 list-disc" v-for="ingredient in ingredients" :key="ingredient">
                        <li>{{ ingredient }}</li>
                    </ul>
                </div>
                <div class="my-2">
                    <p class="font-bold">Instructions:</p>
                    <p>{{ result.strInstructions }}</p>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'ResultModal',
    props: ['result'],
    data() {
        return {
            ingredients: [],
        }
    },
    
    mounted() {
        let count = 1
        for(let i in this.result){
            let ingredient = ''
            let measure = ''
            if (i.startsWith('strIngredient') && this.result[i]) {
                ingredient = this.result[i]
                measure = this.result[`strMeasure` + count]
                count += 1
                this.ingredients.push(`${measure} ${ingredient}`)
            }
        }
    },
}

</script>

<style lang="postcss" scoped>
.modal-container {
    @apply fixed w-full h-full inset-0 z-20 bg-black bg-opacity-60 p-2
}

.modal {
    @apply flex lg:flex-row flex-col items-center bg-white w-3/4 lg:w-4/5 xl:w-2/3 h-[95%] lg:h-[90%] rounded-xl mx-auto my-7 overflow-auto
}

.modal-body {
    @apply flex flex-col w-full h-full lg:w-1/2 p-5 md:p-10 overflow-y-scroll
}

.img-recipe {
    @apply max-w-full py-3 object-cover object-center rounded-xl mx-auto md:mx-5 flex
}
.tag {
    @apply bg-amber-500 text-white mt-3 ml-1 py-1 px-5 w-fit rounded-xl
}
</style>
