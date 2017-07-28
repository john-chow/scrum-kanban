<template>
  <div class="list-group-item taskcard" :class="{ 'task-complete': is_complete == true }" @click="detail_opening = true"> 
    <a href="javascript:;" v-on:click.stop="toggleCompletion" class="task-check" draggable="false">
      <i class="task-check fa fa-square-o" :class="{ 'fa-check-square': is_complete==true }" aria-hidden="true"></i>
    </a> 
    <span class="task-title">{{meta.name}}</span>
    <modal :show.sync="detail_opening" effect="zoom" @mousedown.capture="xxx">
      <div slot="modal-header" class="modal-header">
        <h4 class="modal-title">Modal title</h4>
      </div>
      <div slot="modal-body" class="modal-body">...</div>
    </modal>
  </div>        
</template>

<script>
import {modal} from 'vue-strap'
export default {
  name:  'taskcard',
  props:  ['meta', 'ordernum'],
  data () {
    return {
      uuid:   null,
      is_complete:  false,
      detail_opening:   false,
    }
  },
  components: {
    modal
  },
  methods:  {
    toggleCompletion() {
      this.is_complete = !this.is_complete;
    },
    todelete() {
      debugger;
      this.$emit('deletion', {
        index:  ordernum,
        meta:   meta,
      })
    },
    xxx() {
      debugger;
    }
  },
  created() {
    this.uuid = Date.now();
  }
}
</script>

<style>
  .swimline-content .taskcard {
    position: relative;
    padding: 10px;
    cursor: pointer;
    margin-bottom: 8px;
    background: #fff;
    border-radius: 2px;
    box-shadow: 0 1px 1px rgba(0,0,0,.1)
  }

  .task-check {
    margin-right: 8px;
  }
  .task-complete .task-check {
    color: #69d0d1;
  }
  .task-complete .task-title {
    color: #8f8f8f;
    text-decoration: line-through;
  }
</style>