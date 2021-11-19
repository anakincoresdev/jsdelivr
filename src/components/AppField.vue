<template>
  <input
    :value="modelValue"
    :placeholder="placeholder"
    type="text"
    class="form-control"
    @input="input"
  >
</template>

<script>
export default {
  name: 'AppField',
  props: {
    modelValue: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
  },
  emits: ['update:model-value'],
  methods: {
    input(evt) {
      this.$emit('update:model-value', evt.target.value);
    },
  },
}
</script>
