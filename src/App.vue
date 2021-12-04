<template>
  <v-app>
    <v-main>
      <RandomElements />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import RandomElements from './components/RandomElements.vue'

export default defineComponent({
  name: 'App',

  components: {
    RandomElements
  },

  data () {
    return {
      //
    }
  }
})
</script>
