<script setup lang="ts">
import {ref} from 'vue';

interface Cat {
  id: string;
  url: string;
  width: number;
  height: number;
}
const cat = ref<Cat[]|null>(null);
const isloading = ref(false);
const fetchData = async () => {
  cat.value = null;
  isloading.value = true;
  const response = await fetch("https://api.thecatapi.com/v1/images/search");
  const data: Cat[] = await response.json();
  isloading.value = false;
  cat.value = data;
};

fetchData()

</script>

<template>
  <div>
    <h3>Cuteness Overload</h3>
    <p v-if="isloading">Loading...</p>
    <img v-if="cat" :alt="cat?.[0]?.id" :src="cat?.[0]?.url"  />
    <button @click="fetchData"><p>More</p> <img src="/Cat.png"  /> </button>
  </div>
</template>

<style scoped>
  div {
    margin: 0 auto;
    max-width: 500px;
    max-height: 800px;
    width: 100%;
    height: 100lvh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 2rem;
    gap: 2rem;
  }

  h3 {
    text-transform: uppercase;
    font-size: 2.8rem;
    color: transparent;
    -webkit-text-stroke: 2px #623582;
  }
  img {
    width: 100%;
    max-width: 300px;
    height: 250px;
    object-fit: cover;
    border-radius: 14px;
  }
  button {
    background-color: #F3B5E9;
    outline: none;
    border: none;
    padding: 1rem 2rem;
    border-radius: 14px;
    color: #623582;
    font-size: 18px;
    text-transform: capitalize;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 400;
    gap: 1rem;
  }

  button img {
    width: 28px;
    height: 28px;
    transform: rotate(35deg);
  }
</style>
