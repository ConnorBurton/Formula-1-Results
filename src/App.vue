<template>
  <div id="app">
    <select-race :raceList="raceList" @selectedRaceValue="updateRaceValue" @selectedYearValue="updateYearValue" />
    <current-list :currentRace="currentRace" :spinnerStyle="spinnerStyle" />
  </div>
</template>

<script>
import SelectRace from './components/SelectRace.vue'
import CurrentList from './CurrentList.vue'

import axios from 'axios';

export default {
  name: 'app',
  components: {
    SelectRace,
    CurrentList,
  },
  data() {
    return {
      currentRace: null,
      raceList: null,
      selectedRace: 1,
      selectedYear: 2019,
      spinnerStyle: false,
    }
  },
  mounted() {
    this.getUpdatedRaceResults()
    this.getUpdatedListResults()
  },
  methods: {
    async getUpdatedRaceResults() {
      this.spinnerStyle = true;
      Promise.all([axios.get('https://ergast.com/api/f1/'+ this.selectedYear +'/'+ this.selectedRace +'/results.json')])
        .then(response => {
          this.currentRace = []
          if(response[0].data.MRData.RaceTable.Races[0] !== undefined)
            this.currentRace = response[0].data.MRData.RaceTable.Races[0].Results
          setTimeout( () => this.spinnerStyle = false, 2000)
        })
    },

    async getUpdatedListResults() {
      Promise.all([axios.get('https://ergast.com/api/f1/'+ this.selectedYear +'.json')])
        .then(response => {
          this.currentRace = []
          this.raceList = response[0].data.MRData.RaceTable.Races
      })
    },

    updateYearValue(val) {
      this.selectedYear = val;
      this.selectedRace = 1
      this.getUpdatedListResults()
      this.getUpdatedRaceResults()
    },

    updateRaceValue(val) {
      this.selectedRace = val;
      this.getUpdatedRaceResults()
    }
  }
}
</script>

<style scoped lang="scss">
  #app {
    max-width: 1200px;
    display: block;
    margin: auto;
  }
</style>
