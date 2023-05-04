<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import {ref} from 'vue'
const b = ref<number>(1)

function a(params:number) {
  
  b.value = params
}
</script>

<template>
  <button @click="a( 1)">1</button>
  <button @click="a( 2)">2</button>
  <button @click="a( 3)">3</button>
  <HelloWorld :msg="b" />
</template>

<style scoped>
</style>
