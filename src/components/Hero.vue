<template>
    <section>
    <div class="hero-base">
        <div>
            <h1 class="title">Collection <br> of food <br>recipes</h1>
            <h1 class="title-md">Collection of food recipes</h1>
            <p class="md:text-left text-xl text-center">Recipes to improve and make <br> your cooking even more delicious</p>
        </div>
        <div class="hidden md:block">
            <img class="w-[600px] -mb-36" src="../assets/hero-img.png">
        </div>
    </div>
    </section>
</template>

<style lang="postcss" scoped>
.hero-base{
    @apply bg-amber-500 h-[400px] md:h-[550px] flex flex-col md:flex-row py-14 px-2 sm:px-14 justify-evenly items-center
}

.title{
    @apply hidden md:block text-6xl font-black my-5 capitalize
}

.title-md{
    @apply md:hidden md:text-left text-center text-4xl font-black my-5 capitalize
}
</style>