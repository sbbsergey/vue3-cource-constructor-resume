<template>
  <form className="card card-w30">

    <div className="form-control">
      <label htmlFor="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div className="form-control">
      <label htmlFor="value">Значение</label>
      <textarea id="value"
                rows="3"
                v-model="value"
      ></textarea>
    </div>

    <app-button color="primary"
                :disabled="isDisabledAddComponentButton"
                @action="addComponent(type, value)"
    >Добавить</app-button>

  </form>
</template>

<script>

import AppButton from '@/components/AppButton'

export default {
  emits: {
    addComponent (type, value) {
      let paramIsValid = true
      if (typeof type !== 'string') {
        paramIsValid = false
        console.warn('Неверный параметр type в событии addComponent')
      }
      if (!['title', 'subtitle', 'avatar', 'text'].includes(type)) {
        paramIsValid = false
        console.warn('Неверный параметр type в событии addComponent - проверка по списку')
      }
      if (typeof value !== 'string') {
        paramIsValid = false
        console.warn('Неверный параметр value в событии addComponent')
      }
      return paramIsValid
    }
  },
  data () {
    return {
      type: 'title',
      value: ''
    }
  },
  methods: {
    addComponent (type, value) {
      this.$emit('addComponent', type, value)
      this.value = ''
      this.type = 'title'
    }
  },
  computed: {
    isDisabledAddComponentButton () {
      return this.value.length < 4
    }
  },
  components: { AppButton }
}
</script>
