<template>
  <div class="swimline-wrapper">
    <div class="swimline-content">
      <div class="swimline-header">
        <span class="title">{{meta.name}}</span>
        <i @click="openMenu" class="fa fa-chevron-down action" aria-hidden="true"></i>
      </div>
      <draggable class="list-group swimline-cards" element="div" v-model="tasks" :options="dragOptions" :move="onMoveCard" @start="isDragging=true" @end="isDragging=false"> 
        <taskcard v-for="(one, index) in tasks" :key="index" :meta.sync="one" :ordernum="index" v-on:deletion="deleteCard" v-on:opencard="openCard"></taskcard>
      </draggable>    
      <div class="swimline-footer">
        <item-creator v-on:creation="addCard" text="新建任务"></item-creator>
      </div>
    </div>
    <div v-show="menuOpening" class="menus pbox">
      <ul class="pop-menu">
        <li><a href="javascript:;" @click="rename">...</a></li>
        <li><a href="javascript:;" @click="todelete">删除</a></li>
      </ul>
    </div>
  </div>
</template>

<script>
import Taskcard from './taskcard.vue'
import ItemCreator from './item_creator.vue'
import Draggable from 'vuedraggable'

export default {
  name:   'swimline',
  props:  ['meta', 'ordernum'],
  components: {
    Taskcard,
    ItemCreator,
    Draggable 
  },
  data () {
    return {
      tasks:  [],
      isDragging: false,
      delayedDragging:false,
      menuOpening: false
    }
  },
  computed: {
    dragOptions () {
      return  {
        animation: 0,
        group: 'description',
        ghostClass: 'ghost'
      };
    }
  },
  methods: {
    addCard(option) {
      this.tasks.push({
        name: option.name
      })
    },
    deleteCard(option) {
      let index = option.order;
      this.tasks.splice(index, 1);
    },
    onMoveCard ({relatedContext, draggedContext}) {
      const relatedElement = relatedContext.element;
      const draggedElement = draggedContext.element;
      return (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
    },
    openMenu(e) {
      let ctx = this,
          menu_dom = this.$el.getElementsByClassName('menus')[0];
      menu_dom.style.left = e.x + 'px';
      menu_dom.style.top = (e.y + 10) + 'px';
      this.menuOpening = true;
      setTimeout(() => {
        document.body.addEventListener('click', () => {
          ctx.menuOpening = false;
        }, {once: true});
      }, 1)
    },
    rename() {
    },
    todelete() {
      this.$emit('deletion', {
        order:  this.ordernum,
        meta:   this.meta,
      })
    },
    openCard(option) {
      this.$emit('opencard', option);
    }
  },
  watch:  {
    isDragging (newValue) {
      if (newValue){
        this.delayedDragging= true
        return
      }
      this.$nextTick( () =>{
        this.delayedDragging =false
      })
      console.log('isDragging is changing');
    }
  }
}
</script>

<style>
  .swimline-wrapper {
    width: 280px;
    height: 100%;
    display: inline-block;
    margin: 0 8px;
  }
  .swimline-content {
    display: -webkit-box;
    display: flex;
    display: -ms-flexbox;
    display: -webkit-flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    -ms-flex-direction: column;
    flex-direction: column;
    background: #eaeaea;
    vertical-align: top;
    box-sizing: border-box;
    white-space: nowrap;
    position: relative;
    max-height: 100%;
    border-radius: 3px;
  }
  .swimline-header {
    position: relative;
    padding: 10px 35px 4px 10px;
    cursor: pointer;
    -webkit-box-flex: 0;
    -ms-flex: 0 0 auto;
    flex: 0 0 auto;
    -webkit-flex: 0 0 auto;
  }  
  .swimline-header .title {
    overflow: hidden;
    display: block;
    text-overflow: ellipsis;
    color: #4f555f;
    font-size: 16px;
    font-weight: 700;
    margin-bottom: 6px;
  }
  .swimline-header .action {
    display: block;
    position: absolute;
    right: 8px;
    top: 10px;
    font-size: 16px;
    cursor: pointer;
  }
  .swimline-cards {
    overflow-y: auto;
    overflow-x: hidden;
    min-height: 20px;
    vertical-align: top;
    display: inline-block;
    zoom: 1;
    -webkit-box-flex: 1;
    -ms-flex: 1 1 auto;
    flex: 1 1 auto;
    -webkit-flex: 1 1 auto;
    padding: 0 4px;
    margin: 0 4px 10px;
  }
  .swimline-footer {
    padding: 0 10px 10px;
    -webkit-box-flex: 0;
    -ms-flex: 0 0 auto;
    flex: 0 0 auto;
    -webkit-flex: 0 0 auto;
  }
</style>