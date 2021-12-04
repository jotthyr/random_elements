<template>
  <div class="d-flex justify-space-around align-center flex-column flex-md-row fill-height">
    <v-btn @click="shuffleArray(this.randomArray)" color="white">Randomize</v-btn>
    <input @input="editMode" v-model="editTitle" placeholder="Edit particular title">
  </div>
  <RandomElementsDisplay
  v-on:toggleName="toggleTitle"
  v-for="(row, rowIndex) in this.getRows"
  :key="rowIndex"
  :randomArrayPropsDisplay="this.randomArrayOfArray[rowIndex]">
  </RandomElementsDisplay>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import { Watch } from 'vue-property-decorator'
import _ from 'lodash'
import RandomElementsDisplay from './RandomElementsDisplay/RandomElementsDisplay.vue'

interface IRandomElements {
  id: number,
  title: string
}

@Options({
  components: {
    RandomElementsDisplay
  }
})

export default class RandomElements extends Vue {
  editTitle = '';

  currentId = -1;

  randomArray: Array<IRandomElements> = [
    { id: 1, title: 'title_1' },
    { id: 2, title: 'title_2' },
    { id: 3, title: 'title_3' },
    { id: 4, title: 'title_4' },
    { id: 5, title: 'title_5' },
    { id: 6, title: 'title_6' }
  ];

  rows = 0;

  bufferOne = [] as Array<IRandomElements> ;
  randomArrayOfArray = [] as Array<Array<IRandomElements>>

  get getRows (): number {
    this.rows = Math.floor(this.randomArray.length / 3)

    if (this.randomArray.length % 3 !== 0) {
      this.rows += 1
    }
    return this.rows
  }

  @Watch('randomArray')
  onRandomArrayChange (): void {
    this.randomArrayOfArray = []
    for (let i = 0; i < this.randomArray.length; i += 1) {
      if ((i + 1) % 3 !== 0) {
        this.bufferOne.push(this.randomArray[i])
      } else {
        this.bufferOne.push(this.randomArray[i])
        this.randomArrayOfArray.push(this.bufferOne)
        this.bufferOne = []
      }
      if ((i + 1) === this.randomArray.length) {
        this.randomArrayOfArray.push(this.bufferOne)
        this.bufferOne = []
      }
    }
  }

  beforeCreate (): void {
    for (let i = 0; i < this.randomArray.length; i += 1) {
      if ((i + 1) % 3 !== 0) {
        this.bufferOne.push(this.randomArray[i])
      } else {
        this.bufferOne.push(this.randomArray[i])
        this.randomArrayOfArray.push(this.bufferOne)
        this.bufferOne = []
      }
      if ((i + 1) === this.randomArray.length) {
        this.randomArrayOfArray.push(this.bufferOne)
        this.bufferOne = []
      }
    }
  }

  toggleTitle (id: number): void{
    this.currentId = id
    this.editTitle = ''
  }

  editMode (): void{
    console.log('editmode')
    this.randomArray = this.randomArray.map((item) => {
      if (item.id === this.currentId) {
        return { id: this.currentId, title: this.editTitle }
      }
      return item
    })
  }

  // Creates an array of shuffled values, using a version of the Fisher-Yates shuffle.
  shuffleArray (r: Array<IRandomElements>): void {
    this.randomArray = _.shuffle(r)
  }
}
</script>

<style scoped lang="scss">

</style>
