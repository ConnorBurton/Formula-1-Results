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
      <tbody>
        <tr v-for="detail in currentRace" >
          <td>{{detail.position}}</td>
          <td>{{detail.number}}</td>
          <td>{{detail.Driver.familyName}}</td>
          <td>{{detail.Constructor.name}}</td>
          <td>{{detail.laps}}</td>
          <td v-if="detail.Time !== undefined">{{detail.Time.time}}</td>
          <td v-else>{{detail.status}}</td>
          <td>{{detail.points}}</td>
        </tr>
      </tbody>
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
  }
  thead {
    background: #eee;
  }
  td,th {
    border: 1px solid black;
    padding: 10px;
    border-collapse: collapse;
  }
</style>
