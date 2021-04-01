<template>
  <v-app>
    <v-app-bar
      app
      color="dark"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container grid-list-md>
        <v-layout row wrap>
          <div class="mr-2">Example with string</div>
          <v-flex xs12 lg6>
            <v-text-field
              v-model="date"
              clearable
              label="Date"
              @blur="handleChangeDate(date)"
            >
            </v-text-field>
            <date-picker
              :value="date"
              :mask="mask"
              ref="datepicker"
              @onDateChange="date = $event"
              >
              </date-picker>
          </v-flex>
          <div class="mr-2">Example with array</div>
          <v-flex xs12 lg6>
            <v-text-field
              v-model="dates[0]"
              clearable
              label="From date"
            >
            </v-text-field>
            <v-text-field
              v-model="dates[1]"
              clearable
              label="To date"
              @blur="handleChangeDates(dates)"
            >
            </v-text-field>
            <date-picker
              ref="rangedatepicker"
              :value="dates"
              :mask="mask"
              @onDatesChange="dates = $event"
            >
            </date-picker>
          </v-flex>
        </v-layout>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import DatePicker from './components/DatePicker';

export default {
  name: 'App',
  components: {
    DatePicker
  },
  data: () => ({
    date: '',
    dates: [],
    mask: "DD/MM/YYYY"
  }),
  methods: {
    handleChangeDate (newDate) {
      this.$refs.datepicker.getDate(newDate)
    },
    handleChangeDates (newDates) {
      this.$refs.rangedatepicker.getDates(newDates)
    }
  }
};
</script>
<style>
.container.grid-list-md .layout .flex {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.container.grid-list-md .layout .flex {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.row {
  flex-direction: column;
}
.v-input {
  margin-right: 20px;
}
</style>