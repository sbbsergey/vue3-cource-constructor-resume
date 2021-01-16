<template>
  <component :is="componentName"
             v-bind="{value}"
  ></component>
</template>

<script>

import AppTitle from '@/components/AppTitle'
import AppAvatar from '@/components/AppAvatar'
import AppSubtitle from '@/components/AppSubtitle'
import AppText from '@/components/AppText'

export default {
  props: {
    type: {
      type: String,
      required: true,
      validator (value) {
        return ['title', 'subtitle', 'avatar', 'text'].includes(value)
      }
    },
    value: {
      type: String,
      required: true,
      validator (value) {
        return value.length > 0
      }
    }
  },
  computed: {
    componentName () {
      return 'app-' + this.type
    }
  },
  components: { AppTitle, AppAvatar, AppSubtitle, AppText }
}
</script>
