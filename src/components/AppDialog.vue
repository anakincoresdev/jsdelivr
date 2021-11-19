<template>
  <div
    v-if="modelValue"
    class="bg-black bg-opacity-25 w-100 h-100 top-0 position-fixed fade show"
  >
    <div class="app-dialog__dialog modal-dialog modal-dialog-centered">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">{{ title }}</h5>
          <button
            type="button"
            class="btn-close"
            @click="updateModelValue(false)"
          />
        </div>
        <div class="modal-body">
          <slot />
        </div>
        <div class="modal-footer">
          <slot name="footer">
            <button
              type="button"
              class="btn btn-secondary"
              @click="updateModelValue(false)"
            >
              Закрыть
            </button>
          </slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PackageInfoDialog',
  props: {
    modelValue: {
      type: Boolean,
      default: false,
    },
    title: {
      type: String,
      default: '',
    },
  },
  emits: ['update:model-value'],
  methods: {
    updateModelValue(value) {
      this.$emit('update:model-value', value);
    },
  },
}
</script>

<style lang="scss" scoped>
  .app-dialog {
    &__dialog {
      max-width: 700px;
    }
  }
</style>
