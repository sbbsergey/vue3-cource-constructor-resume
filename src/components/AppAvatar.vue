<template>
  <div className="avatar">
    <img :src=value>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true,
      default: ''
    }
  }
}
</script>

<style scoped>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
