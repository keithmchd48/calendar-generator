<template>
  <div id="app">
    <div class="main-wrapper">
      <div class="selector-wrapper">
        <label>
          <select v-model="selectedMonth">
            <option v-for="(month) in months" :key="month" :value="month">
              {{getMonth(month)}}
            </option>
          </select>
        </label>
        <label>
          <select v-model="selectedYear">
            <option v-for="(year) in years" :key="year" :value="year">
              {{year}}
            </option>
          </select>
        </label>
      </div>
      <div class="month-wrapper">
        <Month :month="selectedMonth" :year="selectedYear"></Month>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment/moment'
import Month from "@/components/Month";
export default {
  name: 'App',
  components: {Month},
  data () {
    return {
      selectedMonth: '0',
      selectedYear: '2010',
      months: [
        '0',
        '1',
        '2',
        '3',
        '4',
        '5',
        '6',
        '7',
        '8',
        '9',
        '10',
        '11'
      ],
      years: [
        '2010',
        '2011',
        '2012',
        '2013',
        '2014',
        '2015',
        '2016',
        '2017',
        '2018',
        '2019',
        '2020'
      ]
    }
  },
  methods: {
    getMonth (monthNum) {
      return moment().month(parseInt(monthNum)).format("MMMM")
    }
  }
}
</script>

<style scoped>
  #app {
    background-color: blanchedalmond;
    height: 100vh;
    /*width: 100vw;*/
  }
  .main-wrapper {
    margin: 0 auto;
    padding: 3rem 10px;
    max-width: 900px;
  }
  .selector-wrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  select {
    font-size: 1rem;
    border-radius: 4px;
    border: 1px solid lightgrey;
    outline: none;
    width: 8rem;
    height: 2.2rem;
    padding: 3px 4px;
    cursor: pointer;
  }
  .month-wrapper {
    margin-top: 1rem;
  }
  @media only screen and (min-width: 460px) {
    label + label {
      margin-left: 2rem;
    }
  }
</style>
