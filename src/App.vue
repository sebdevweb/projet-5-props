<template>
  <One :datas="datas" v-if="datas" />
  <Two :datas="datas" v-if="datas" />
  <Three :datas="datas" v-if="datas" />
</template>


<script setup>
  import { onMounted, ref } from 'vue';
  import One from './components/One.vue';
  import Two from './components/Two.vue';
  import Three from './components/Three.vue';

  const datas = ref(null)
  const state = ref('loading')

  onMounted(() => {
    fetch('/datas.json')
      .then( response => {
        if (response.ok)  {
          return response.json()
        }
        throw new Error('Impossible de récupérer le json')
      })
      .then(data => {
        datas.value = data
        state.value = 'idle'
      })
      .catch(error => {
        state.value = 'error'
      })
  })

</script>


<style lang="scss">

</style>
