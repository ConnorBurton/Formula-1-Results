<template>
  <div id="select-race">
    <select class="select-year" name="" v-model="selectedYear" @change="onChangeYear($event)">
      <option v-for="year in years" :value="year">{{year}}</option>
    </select>

    <select class="select-race" name="" v-model="selectedRace" @change="onChangeRace($event)">
      <option >Select Race</option>
      <option v-for="race in raceList" :value="race.round">{{ race.raceName }}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'select-race',
  data() {
    return {
      selectedRace: 1,
      selectedYear: '',
    }
  },
  props: {
    raceList: Array
  },
  beforeMount() {
    this.selectedYear = new Date().getFullYear()
  },
  methods: {
    onChangeYear(event) {
      this.$emit('selectedYearValue', event.target.value)
    },
    onChangeRace(event) {
      this.$emit('selectedRaceValue', event.target.value)
    }
  },
  computed : {
    years() {
      const year = new Date().getFullYear()
      return Array.from({length: year - 1949}, (value, index) => 1950 + index)
    }
  }
}
</script>


<style scoped></style>
