<template>
  <div id="app">
    <select-race :raceList="raceList" @selectedRaceValue="updateRaceValue" @selectedYearValue="updateYearValue" />
    <current-list :currentRace="currentRace" />
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
    }
  },
  mounted() {
    this.getUpdatedRaceResults()
    this.getUpdatedListResults()
  },
  methods: {
    getUpdatedRaceResults: function() {
      Promise.all([axios.get('http://ergast.com/api/f1/'+ this.selectedYear +'/'+ this.selectedRace +'/results.json')])
        .then(response => {
          this.currentRace = []
          this.currentRace = response[0].data.MRData.RaceTable.Races[0].Results
      })
    },

    getUpdatedListResults: function() {

      Promise.all([axios.get('http://ergast.com/api/f1/'+ this.selectedYear +'.json')])
        .then(response => {
          this.currentRace = []
          this.raceList = response[0].data.MRData.RaceTable.Races
      })

      // axios
      //   .get('http://ergast.com/api/f1/'+ this.selectedYear +'.json')
      //   .then(response => (this.raceList = response.data.MRData.RaceTable.Races))
    },

    updateYearValue(val) {
      this.selectedYear = val;
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

<style scoped>
  #app {
    max-width: 1200px;
    display: block;
    margin: auto;
  }
</style>
