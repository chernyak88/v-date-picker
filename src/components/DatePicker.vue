<template>
  <v-menu
    v-model="menu"
    :close-on-content-click="false"
    max-width="290"
  >
    <template v-slot:activator="{ on }">
      <v-icon
        medium
        v-on="on"
      >
        mdi-calendar
      </v-icon>
    </template>
    <v-date-picker v-if="isArray"
      v-model="localValue"
      first-day-of-week="1"
      header-color="#1E1E1E"
      range
      @change="setDates"
    >
    </v-date-picker>
    <v-date-picker v-else
      v-model="localValue"
      first-day-of-week="1"
      header-color="#1E1E1E"
      @change="setDate"
    ></v-date-picker>
  </v-menu>
</template>

<script>
import moment from 'moment'

export default {
  name: 'DatePicker',
  props: {
    value: [String, Array],
    mask: String
  },
  data: () => ({
    localValue: null,
    isValid: false,
    menu: false,
    isArray: false,
    curDate: moment().format('YYYY-DD-MM'),
    fromDate: moment().format(),
    toDate: moment().add(7,'d').format()
  }),
  mounted() {
    if(Array.isArray(this.value)) {
      this.isArray = true
      this.localValue = [this.fromDate, this.toDate]
      this.setDates()
    } else {
      this.localValue = this.curDate
      this.setDate()
    }
  },
  methods: {
    setDates () {
        this.menu = false
        const formattedValue = this.localValue.sort().map(date => moment(date).format(this.mask))
        this.$emit('onDatesChange', formattedValue)
    },
    setDate () {
        this.menu = false
        this.$emit('onDateChange', moment(this.localValue).format(this.mask))
    },
    getDate (val) {
      if(moment(val).isValid()) {
        this.localValue = moment(val).format('YYYY-DD-MM')
        this.setDate()
      } else {
        this.localValue = this.curDate
        this.setDate()
      }
    },
    getDates (val) {
      if(moment(val[0]).isValid() && moment(val[1]).isValid()) {
        this.localValue = [moment(val[0]).format('YYYY-DD-MM'), moment(val[1]).format('YYYY-DD-MM')]
        this.setDates()
      } else {
        this.localValue = [this.fromDate, this.toDate]
        this.setDates()
      }
    }
  }
}
</script>
<style scoped>
.v-icon.v-icon.v-icon--link {
  width: 24px;
  height: 24px;
  margin-left: -10px;
}
</style>