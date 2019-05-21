<template>
  <div id="current-table">
    <table>
      <thead>
        <tr>
          <th>Position</th>
          <th>Number</th>
          <th>Driver</th>
          <th>Constructor</th>
          <th>Laps</th>
          <th>Time</th>
          <th>Points</th>
        </tr>
      </thead>
      <tbody v-if="currentRace !== ''">
        <tr v-for="detail in currentRace" >
          <td class="position">{{detail.position}}</td>
          <td class="number">{{detail.number}}</td>
          <td class="name">{{detail.Driver.familyName}}</td>
          <td class="constructor">{{detail.Constructor.name}}</td>
          <td class="laps">{{detail.laps}}</td>
          <td v-if="detail.Time !== undefined" class="time">{{detail.Time.time}}</td>
          <td v-else class="time">{{detail.status}}</td>
          <td class="points">{{detail.points}}</td>
        </tr>
      </tbody>
      <div v-else>
        No Results
      </div>
    </table>
  </div>

</template>

<script>
    export default {
    name: 'current-table',
    props: {
      currentRace: Array,
    }
  }
</script>

<style scoped>
  table {
    width: 100%;
    border-spacing: 0;
    border: 0px;
  }
  thead {

  }
  tr {
    border-bottom: 1px solid #444;
  }
  td,th {
    padding: 35px 15px;
    color: #fff;
    text-align: center;
    font-weight: 100;
    letter-spacing: 0.5px;
  }
  th {
    font-weight: 600;
    padding: 25px 15px;
  }
  .position, .number {
    width: 115px;
  }
</style>
