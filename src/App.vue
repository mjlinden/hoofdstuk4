<template>
  <div id="app" class="container">
    <Countries/>
    <Invoervak/>
    <Filtering/>
  </div>
</template>

<script>
import Countries from './components/Countries.vue'
import Invoervak from './components/Invoervak.vue'
import Filtering from './components/Filtering.vue'

export default {
  name: 'App',
  components: {
      Countries,
      Invoervak,
      Filtering
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
