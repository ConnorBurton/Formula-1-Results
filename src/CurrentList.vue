<template>
  <div id="current-table">

    <div class="spinner" :class="{ 'visible' : spinnerStyle}"></div>

    <div :class="['results-wrapper', { 'hidden' : spinnerStyle}]">
      <table v-if="currentRace !== null && currentRace.length !== 0">
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
      </table>
      <div v-else class="no-results">
        <p>No results were found, please select a different race</p>
      </div>
    </div>

  </div>
</template>

<script>
    export default {
    name: 'current-table',
    props: {
      currentRace: Array,
      spinnerStyle: Boolean,
    }
  }
</script>

<style scoped lang="scss">
  #current-table {
    position: relative;
  }

  .results-wrapper {
    transform: none;
    opacity: 1;
    visibility: visible;
    transition: .75s ease;
    &.hidden {
      transform: translateY(60px);
      opacity: 0;
      visibility: hidden;
      transition: .3s ease;
    }
  }

  table {
    width: 100%;
    border-spacing: 0;
    border: 0px;
    tr {
      border-bottom: 1px solid #444;
      td,th {
        padding: 35px 15px;
        color: #fff;
        text-align: center;
        font-weight: 100;
        letter-spacing: 0.5px;
        &.position, &.number {
          width: 115px;
        }
      }
      th {
        font-weight: 600;
        padding: 25px 15px;
      }
    }
  }

  .no-results {
    display: block;
    text-align: center;
    padding-top: 40px;
    p {
      color: #fff;
      font-size: 24px;
      font-weight: 700;
    }
  }

  .spinner {
    position: absolute;
    top: 40px;
    left: 50%;
    transform: translateX(-50%);
    width: 100px;
    height: 100px;
    background-image: url(https://thumbs.gfycat.com/BogusEmptyBrontosaurus-max-1mb.gif);
    background-position: center;
    background-repeat: no-repeat;
    background-size: contain;
    opacity: 0;
    visibility: hidden;
    transition: .3s ease;
    &.visible {
      opacity: 1;
      visibility: visible;
    }
  }
</style>
