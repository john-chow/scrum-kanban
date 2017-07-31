<template>
  <modal :show.sync="opening" effect="zoom">
    <div slot="modal-header" class="modal-header">
      <h4 class="modal-title">Modal title</h4>
    </div>
    <div slot="modal-body" class="modal-body">...</div>
  </modal>
</template>

<script>
import {modal} from 'vue-strap'
export default {
  name:  'taskdetail',
  props:  ['opening'],
  components: {
    modal
  },
  data () {
    return {
    }
  },
}
</script>

<style>
</style>