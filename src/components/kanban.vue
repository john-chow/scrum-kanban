<template>
  <div>
    <div>
      <swimline v-for="one in matters">
      </swimline>
    </div>
    <div>
      <item-creator text="新建列表"></item-creator>
    </div>
  </div>
</template>

<script>
import Swimline from './swimline.vue'
import ItemCreator from './item_creator.vue'
import 'bootstrap/dist/css/bootstrap.css'

export default {
  name:  'kanban',
  components: {
    Swimline,
    ItemCreator
  },
  data () {
    return {
      matters:   []
    }
  }
}
</script>

<style>
</style>