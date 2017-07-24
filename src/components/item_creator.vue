<template>
  <div class="entry-new">
    <div v-if="is_creating">
      <div class="form-group">
        <input type="text" v-model="name" class="form-control">
      </div>
      <div class="form-group">
        <button class="btn btn-primary" @click="create">确定</button>
        <button class="btn btn-link" @click="cancel">取消</button>
      </div>
    </div>
    <div v-if="!is_creating">
      <a href="javascript:;" class="btn-add" @click="is_creating = !is_creating">
        <i class="lcfont lc-add"></i>{{text}}
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
      // request post 提交保存
      this.$emit('creation', {name: this.name});
      this.name = '';
      this.is_creating = false;
    },
    cancel() {
      this.is_creating = false;
    }
  }
}
</script>

<style>
  .btn-add {
    display: block;
    color: #8f8f8f;
  }
</style>