<template>
  <app-loader v-if="loading"></app-loader>
  <template v-else>
    <p v-if="commentsIsEmpty">
      <app-button color="primary"
                  @action="loadComments"
      >Загрузить комментарии</app-button>
    </p>
    <div className="card" v-else>
      <h2>Комментарии</h2>
      <ul className="list">
        <li className="list-item" v-for="{id,email,body} in comments" :key="id">
          <div>
            <p><strong>{{ email }}</strong></p>
            <small>{{ body }}</small>
          </div>
        </li>
      </ul>
    </div>
  </template>

</template>

<script>

import axios from 'axios'
import AppLoader from '@/components/AppLoader'
import AppButton from '@/components/AppButton'

export default {
  data () {
    return {
      comments: [],
      loading: false
    }
  },
  methods: {
    loadComments () {
      this.loading = true
      setTimeout(async () => {
        try {
          const { data } = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
          if (!data) {
            throw new Error('Список комментариев пуст!')
          }
          this.comments = Object.keys(data).map(key => {
            return {
              id: key,
              ...data[key]
            }
          })
          this.loading = false
        } catch (e) {
          this.loading = false
        }
      }, 2000)
    }
  },
  computed: {
    commentsIsEmpty () {
      return this.comments.length === 0
    }
  },
  components: { AppLoader, AppButton }
}
</script>
