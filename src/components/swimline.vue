<template>
  <div class="swimline-wrapper">
    <div class="swimline-content">
      <div class="swimline-header">
        <span class="title">{{meta.name}}</span>
      </div>
      <div class="swimline-cards">
        <card v-for="one in things" :meta.sync="one"></card>
      </div>
      <div class="swimline-footer">
        <item-creator v-on:creation="addThing" text="新建任务"></item-creator>
      </div>
    </div>
  </div>
</template>

<script>
import Card from './card.vue'
import ItemCreator from './item_creator.vue'

export default {
  name:   'swimline',
  props:  ['meta'],
  components: {
    Card,
    ItemCreator
  },
  data () {
    return {
      things:  []
    }
  },
  methods: {
    addThing(option) {
      this.things.push({
        name: option.name
      })
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
    font-weight: 500;
    margin-bottom: 6px;
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