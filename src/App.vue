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
      axios
        .get('http://ergast.com/api/f1/'+ this.selectedYear +'/'+ this.selectedRace +'/results.json')
        .then(response => (this.currentRace = response.data.MRData.RaceTable.Races[0].Results))
    },

    getUpdatedListResults: function() {
      axios
        .get('http://ergast.com/api/f1/'+ this.selectedYear +'.json')
        .then(response => (this.raceList = response.data.MRData.RaceTable.Races))
    },

    updateYearValue(val) {
      this.currentRace = '';
      this.selectedYear = val;
      this.getUpdatedListResults()
      this.getUpdatedRaceResults()
    },

    updateRaceValue(val) {
      this.currentRace = '';
      this.selectedRace = val;
      this.getUpdatedRaceResults()
    }
  }
}
</script>

<style>

</style>
