<template>
  <button class="btn"
          :class="color"
          @click.prevent="$emit('action')"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  emits: ['action'],
  props: {
    color: {
      type: String,
      required: true,
      default: '',
      validator (value) {
        return ['', 'primary'].includes(value)
      }
    }
  }
}
</script>
