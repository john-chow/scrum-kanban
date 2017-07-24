<template>
  <div>
    <div v-for="one in things">
    </div>
  </div>
</template>

<script>
import Card from './card.vue'
export default {
  name:  'swimline',
  components: {
    Card
  },
  data () {
    return {
      things:  []
    }
  }
}
</script>

<style>
</style>