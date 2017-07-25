<template>
  <div class="task-board">
    <div class="district">
      <swimline class="sortable-item" v-for="(one, index) in matters" :meta.sync="one" :ordernum="index" v-on:deletion="deleteMatter">
      </swimline>
    </div>
    <item-creator v-on:creation="addMatter" text="新建列表"></item-creator>
  </div>
</template>

<script>
import 'bootstrap'
import Swimline from './swimline.vue'
import ItemCreator from './item_creator.vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'font-awesome/css/font-awesome.css'

export default {
  name:  'kanban',
  components: {
    Swimline,
    ItemCreator
  },
  data () {
    return {
      matters:   [{
        name:   'todo'
      }, {
        name:   'doing'
      }]
    }
  },
  methods:  {
    addMatter(option) {
      this.matters.push({
        name: option.name
      })
    },
    deleteMatter(option) {
      let index = option.order;
      this.matters.splice(index, 1);
    }
  },
  mounted:   function() {
    let ctx = this,
      $district = this.$el.getElementsByClassName('district')[0];
    Sortable.create($district, {
      draggable: '.sortable-item',
      handle:    '.swimline-header',
      onEnd (evt) {
        let swimlines = ctx.swimlines;
        ctx.swimlines = [];

        setTimeout(() => {
          let item = swimlines[evt.oldIndex];
          swimlines.splice(evt.oldIndex, 1);
          swimlines.splice(evt.newIndex, 0, item);

          ctx.swimlines = swimlines;
        }, 0)
      }
    });
  },
}
</script>

<style>
.task-board {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  white-space: nowrap;
  overflow-y: hidden;
  overflow-x: auto;
}
</style>