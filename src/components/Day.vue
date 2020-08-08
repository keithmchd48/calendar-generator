<template>
  <div class="component-container non-today">
    {{formatDate}}
  </div>
</template>

<script>
  import moment from 'moment/moment'
  export default {
    name: 'Day',
    props: {
      date: {
        type: String,
        required: true
      }
    },
    computed: {
      // presents the date in "10" format
      formatDate () {
        if (!this.date) {
          return ''
        }
        return moment(this.date).format('DD')
      }
    }
  }
</script>
<style scoped>
  .component-container {
    display: flex;
    justify-content: center;
    align-items: center;
    border-width: 1px;
    height: 100%;
    width: 100%;
    padding: 2rem 0;
    background-color: white;
    cursor: pointer;
    transition: background-color 0.2s ease-in;
  }
  .component-container:hover {
    background-color: lightgray;
  }
  .non-today {
    border-bottom-style: solid;
    border-bottom-color: lightgrey;
    border-right-style: solid;
    border-right-color: lightgrey;
  }
  @media only screen and (max-width: 460px) {  }
</style>
