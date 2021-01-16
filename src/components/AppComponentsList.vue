<template>
  <div className="card card-w70">
    <template v-if="componentsIsNotEmpty">
      <app-component v-for="{type,value,id} in components"
                     :key="id"
                     v-bind="{type,value}"
      ></app-component>
    </template>
    <h3 v-else
    >Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>

import AppComponent from '@/components/AppComponent'

export default {
  props: {
    components: {
      type: Array,
      required: true
    }
  },
  computed: {
    componentsIsNotEmpty () {
      return this.components.length !== 0
    }
  },
  components: { AppComponent }
}
</script>
