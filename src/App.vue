<template>
  <div className="container column">
    <app-constructor @addComponent="addComponent"></app-constructor>
    <app-loader v-if="loading"></app-loader>
    <app-components-list v-else
                         :components="components"
    ></app-components-list>
  </div>
  <div className="container">
    <app-comments></app-comments>
  </div>
</template>

<script>

import axios from 'axios'
import AppConstructor from '@/components/AppConstructor'
import AppComponentsList from '@/components/AppComponentsList'
import AppComments from '@/components/AppComments'
import AppLoader from '@/components/AppLoader'

export default {
  data () {
    return {
      components: [],
      loading: false
    }
  },
  mounted () {
    this.loadComponents()
  },
  methods: {
    async addComponent (type, value) {
      const response = await fetch('https://vue-constructor-resume-default-rtdb.firebaseio.com/components.json', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          type: type,
          value: value
        })
      })
      const firebaseData = await response.json()
      this.components.push({
        id: firebaseData.name,
        type: type,
        value: value
      })
    },
    async loadComponents () {
      try {
        this.loading = true
        const { data } = await axios.get('https://vue-constructor-resume-default-rtdb.firebaseio.com/components.json')
        if (data) {
          this.components = Object.keys(data).map(key => {
            return {
              id: key,
              ...data[key]
            }
          })
        }
        this.loading = false
      } catch (e) {
        this.loading = false
      }
    }
  },
  components: { AppConstructor, AppComponentsList, AppComments, AppLoader }
}
</script>
