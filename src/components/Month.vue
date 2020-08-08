<template>
  <section class="section-grid">
    <div class="calendar-grid">
      <div v-for="(day) in weekdays"
           :key="day.dy"
           class="week-day">
        {{day.dy}}
      </div>
      <Day v-for="(each, index) in monthLoop" :key="index"
               :date="each">
      </Day>
    </div>
  </section>
</template>

<script>
  import Day from './Day'
  import moment from 'moment/moment'
  export default {
    name: "Month",
    components: {Day},
    props: {
      month: {
        type: String,
        required: true
      },
      year: {
        type: String,
        required: true
      }
    },
    data () {
      return {
        weekdays: [
          {dy: 'Mon'},
          {dy: 'Tue'},
          {dy: 'Wed'},
          {dy: 'Thu'},
          {dy: 'Fri'},
          {dy: 'Sat'},
          {dy: 'Sun'}
        ]
      }
    },
    computed: {
      startDate () {
        return moment([Number(this.year), Number(this.month)]).format()
      },
      lastDate () {
        return moment(this.startDate).endOf('month').format()
      },
      monthLoop () {
        // determine previous monday date
        const firstWeekMonday = moment(this.startDate).isoWeekday(1).format()
        // determine all dates from firstWeekMonday to start of the month
        let preOffsetDays = this.generateDates(firstWeekMonday, moment(this.startDate).add(-1, 'days').format())
        preOffsetDays = preOffsetDays.map(() => {
          return ''
        })
        // get sunday of last week of the month
        const lastWeekSunday = moment(this.lastDate).isoWeekday(7).format()
        // determine all dates from last day of the month to lastWeekSunday
        let suffOffsetDays = this.generateDates(moment(this.lastDate).add(1, 'days').format(), lastWeekSunday)
        suffOffsetDays = suffOffsetDays.map(() => {
          return ''
        })
        let propsArr = this.generateDates(this.startDate, this.lastDate)
        propsArr = propsArr.map(d => d)
        return [...preOffsetDays, ...propsArr, ...suffOffsetDays]
      }
    },
     methods: {
       generateDates (start, end) {
         let arr = []
         let st = moment(start)
         let edt = moment(end)
         // eslint-disable-next-line no-unmodified-loop-condition
         while (st.isSameOrBefore(edt)) {
           arr.push(moment(st).format())
           st = moment(st).add(1, 'days')
         }
         return arr
       }
     }
  }
</script>

<style scoped>
  .week-day {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: lightskyblue;
    color: white;
    border-radius: 4px;
  }
  .calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, minmax(48px, 100%));
    grid-column-gap: 2px;
    grid-row-gap: 3px;
    width: 100%;
  }
  @media only screen and (max-width: 460px) {
    .calendar-grid, .section-grid {
      overflow-x: scroll;
    }
  }
</style>
