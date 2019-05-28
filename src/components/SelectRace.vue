<template>
  <div id="select-race">
    <select class="select-year" name="" v-model="selectedYear" @change="onChangeYear($event)">
      <option v-for="year in years" :value="year">{{year}}</option>
    </select>

    <select id="raceSelect" name="" v-model="selectedRace" @change="onChangeRace($event)">
      <option v-for="race in raceList" :value="race.round">{{ race.raceName }}</option>
    </select>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'select-race',
  data() {
    return {
      selectedRace: null,
      latestRace: null,
      selectedYear: '',
    }
  },
  props: {
    raceList: Array
  },
  beforeMount() {
    this.getLatestRace()
    this.selectedYear = new Date().getFullYear()
  },
  methods: {
    async getLatestRace() {
      Promise.all([axios.get('http://ergast.com/api/f1/current/last.json')])
        .then(response => {
          this.latestRace = response[0].data.MRData.RaceTable.round
          this.selectedRace = response[0].data.MRData.RaceTable.round
        })
    },

    onChangeYear(event) {
      this.$emit('selectedYearValue', event.target.value)
      this.selectedRace = 1
    },
    onChangeRace(event) {
      this.$emit('selectedRaceValue', event.target.value)
    }
  },
  computed: {
    years() {
      const year = new Date().getFullYear()
      return Array.from({length: year - 1949}, (value, index) => 1950 + index)
    }
  }
}
</script>


<style scoped lang="scss">
  #select-race {
    text-align: center;
    padding: 40px 0 50px;
    select {
      appearance: none;
      margin: 0 20px;
      color: #fff;
      border: 0px;
      border-bottom: 1px solid #fff;
      padding: 15px 50px;
      background-color: #212121;
      border-radius: 0;
      outline: none;
      text-align-last: center;
    }
  }
</style>
