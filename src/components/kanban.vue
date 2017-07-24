<template>
  <div class="task-board">
    <div class="district">
      <swimline v-for="one in matters" :meta.sync="one">
      </swimline>
    </div>
    <item-creator v-on:creation="addMatter" text="新建列表"></item-creator>
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
  },
  methods:  {
    addMatter(option) {
      this.matters.push({
        name: option.name
      })
    }
  }
}
</script>

<style>
</style>