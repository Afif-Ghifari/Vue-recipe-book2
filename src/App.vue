<template>
  <main class="min-h-screen">
    <Header />
    <Hero />
    <section>
      <InputSearch @startSearch="handleSearch"/>
      <ResultList ref="resultLists"/>
    </section>
  </main>
</template>

<script setup>
import { ref } from 'vue';
import 'bootstrap-icons/font/bootstrap-icons.css'
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import InputSearch from './components/InputSearch.vue'
import ResultList from './components/results/ResultList.vue'

const resultLists = ref(null)

const handleSearch = (keyword) => {
  resultLists.value.startSearch(keyword)
}
</script>

<style>

</style>
