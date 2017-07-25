<template>
  <div class="list-group-item taskcard" :class="{ 'task-complete': is_complete == true }" @click="openDetail"> 
    <a href="javascript:;" @click="toggleCompletion" class="task-check" draggable="false">
      <i class="task-check fa fa-square-o" :class="{ 'fa-check-square': is_complete==true }" aria-hidden="true"></i>
    </a> 
    <span class="task-title">{{meta.name}}</span>
    <div class="card-detail modal-dialog modal-lg" style="display: none;">
      <div class="modal-content">
        <div>{{meta.name}}</div>
        <div class="modal-footer">
          <button type="button" class="btn btn-default" @click="closeDetail">取消</button>
          <button type="button" class="btn btn-primary">保存</button>
        </div>
      </div>
    </div>
  </div>        
</template>

<script>
export default {
  name:  'taskcard',
  props:  ['meta'],
  data () {
    return {
      is_complete:  false,
    }
  },
  methods:  {
    toggleCompletion() {
      this.is_complete = !this.is_complete;
    },
    openDetail() {
      let dom = this.$el.getElementsByClassName('card-detail')[0];
      /*
      dom.removeClassName('zoomOut');
      dom.addClassName('zoomIn');
      */
    },
    closeDetail() {
      let dom = this.$el.getElementsByClassName('card-detail')[0];
      dom.removeClassName('zoomIn');
      dom.addClassName('zoomOut');
    }
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