<template>
  <div class="taskcard">
    {{meta.name}}
  </div>
</template>

<script>
export default {
  name:  'card',
  props:  ['meta'],
  data () {
    return {
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
</style>