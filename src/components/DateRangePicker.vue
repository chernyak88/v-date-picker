<template>
  <v-container grid-list-md>
    <v-layout row wrap>
      <v-flex xs12 lg6>
        <v-menu
          v-model="menu"
          :close-on-content-click="false"
          max-width="290"
        >
          <template v-slot:activator="{ on }">
            <v-text-field
              :value="dateFromFormatted"
              clearable
              label="From date"
              v-on="on"
              readonly
            >
            </v-text-field>
            <v-text-field
              :value="dateToFormatted"
              clearable
              label="To date"
              v-on="on"
              append-icon="mdi-calendar"
              readonly
            >
            </v-text-field>
          </template>
          <v-date-picker
            v-model="rangeDates"
            range
            @change="handleChange"
            first-day-of-week="1"
            header-color="#1E1E1E"
          ></v-date-picker>
        </v-menu>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import moment from 'moment'
export default {
  name: 'DateRangePicker',
  props: {
    onDatesChange: {
      type: Function,
      required: true
    }
  },
  data: () => ({
    rangeDates: [
      new Date().toISOString().substr(0, 10),
      new Date().toISOString().substr(0, 10)
    ],
    menu: false
  }),
  computed: {
    dateFromFormatted () {
      return moment(this.rangeDates[0]).format('DD/MM/YYYY')
    },
    dateToFormatted () {
      return moment(this.rangeDates[1]).format('DD/MM/YYYY')
    }
  },
  methods: {
    handleChange () {
      this.menu = false
      this.onDatesChange([this.dateFromFormatted, this.dateToFormatted])
    }
  }
}
</script>

<style scoped>
.container.grid-list-md .layout .flex {
  display: flex;
  justify-content: space-between;
}
.v-input {
  max-width: 45%;
}
</style>