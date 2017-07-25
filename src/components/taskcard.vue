<template>
  <div class="list-group-item taskcard" :class="{ 'task-complete': is_complete == true }" @click.self="openDetail"> 
    <a href="javascript:;" v-on:click.stop="toggleCompletion" class="task-check" draggable="false">
      <i class="task-check fa fa-square-o" :class="{ 'fa-check-square': is_complete==true }" aria-hidden="true"></i>
    </a> 
    <span class="task-title">{{meta.name}}</span>
    <div class="modal fade" :id="[uuid]" tabindex="-1" role="dialog" v-on:click.stop="uuid=uuid">
      <div class="modal-dialog modal-lg" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
            <h4 class="modal-title" id="gridSystemModalLabel">{{meta.name}}</h4>
          </div>
          <div class="modal-body"> 
            <button type="button" class="btn btn-default" @click="todelete">删除</button>
          </div>
        </div>
      </div>
    </div>
  </div>        
</template>

<script>
export default {
  name:  'taskcard',
  props:  ['meta', 'ordernum'],
  data () {
    return {
      uuid:   null,
      is_complete:  false,
    }
  },
  methods:  {
    toggleCompletion() {
      this.is_complete = !this.is_complete;
    },
    openDetail() {
      let id = '#' + this.uuid;
      $(id).modal();
    },
    closeDetail() {
    },
    todelete() {
      debugger;
      this.$emit('deletion', {
        index:  ordernum,
        meta:   meta,
      })
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