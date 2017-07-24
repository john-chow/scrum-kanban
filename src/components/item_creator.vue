<template>
  <div>
    <div v-if="is_creating">
      <div class="form-group">
        <input type="text" v-model="name">
      </div>
      <div class="form-group">
        <button class="btn btn-primary" @click="create">确定</button>
        <button class="btn btn-link" @click="cancel">取消</button>
      </div>
    </div>
    <div v-if="!is_creating">
      <a href="javascript:;" class="btn-add" @click="is_creating = !is_creating">
        <i class="lcfont lc-add"></i>新建列表
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name:  'item-creator',
  props:  ['text'],
  data () {
    return {
      is_creating:  false,
      name:         ''
    }
  },
  methods:  {
    create() {
    },
    cancel() {
    }
  }
}
</script>

<style>
</style>