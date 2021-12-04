<template>
    <v-item-group selected-class="primary">
      <v-container>
        <v-row>
          <v-col
            v-for="(n, nIndex) in this.randomArrayPropsDisplay"
            :key="n"
            cols="12"
            md="4"
          >
            <v-item v-slot="{ selectedClass}">
              <v-card
                :class="['d-flex flex-nowrap align-center', selectedClass]"
                dark
                height="200"
                @click="this.toggle(this.randomArrayPropsDisplay[nIndex].id)"
              >
                <v-scroll-y-transition>
                  <div
                    v-if="true"
                    class="text-h2 flex-grow-1 text-center"
                  >
                  <h2 class="itemCard__caption">{{this.randomArrayPropsDisplay[nIndex].title}}</h2>
                  </div>
                </v-scroll-y-transition>
              </v-card>
            </v-item>

          </v-col>
        </v-row>
      </v-container>
    </v-item-group>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'RandomElementsDisplay',
  props: {
    randomArrayPropsDisplay: {
      type: Array
    }
  },
  setup () {
    // const readersNumber = ref(0);
    // const book = reactive({ title: "Vue 3 Guide" })

    function toggle (id) {
      this.$emit('toggleName', id)
    }

    return {
      toggle
    }
  }
})
</script>

<style scoped lang="scss">

.itemCard{
  &__caption{
  position: relative !important;
  left: 0px !important;
  z-index: 999 !important;
  }
}

</style>
