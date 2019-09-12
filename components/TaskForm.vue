<template>
  <div class="modal" v-bind:class="{'is-active': isActive}">
    <div class="modal-background"></div>
    <div class="modal-content">
      <div class="card">
        <div class="card-content">
          <p class="title">Catatan</p>
          <div class="field">
            <div class="control">
              <textarea class="textarea" placeholder="Task, Catatan Kecil, dll...">{{ value }}</textarea>
            </div>
          </div>
          <div class="field">
            <div class="control">
              <button class="button is-primary">Simpan</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <button class="modal-close is-large" aria-label="close" @click="$emit('close')"></button>
  </div>
</template>

<script>
export default {
  name: 'TaskForm',
  props: {
    value: {
      type: String,
      required: true,
      default: ''
    },
    isActive: {
      type: Boolean,
      required: true,
      default: false
    }
  }
}
</script>
