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
              :value="singleDateFormatted"
              clearable
              label="Date"
              append-icon="mdi-calendar"
              v-on="on"
              @change="handleInputChange"
            >
            </v-text-field>
          </template>
          <v-date-picker
            v-model="singleDate"
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
// Для наглядности компонент разбит на два файла.
// При необходимости можно объединить всю верстку и логику в один файл,
// и отрисовывать необходимую часть через v-if, например, в зависимости
// от приходящего пропса (если он есть, отображаем DatePicker с диапазоном
// дат, если нет - обычный)
import moment from 'moment'
export default {
  name: 'DatePicker',
  props: {
    onDateChange: {
      type: Function,
      required: true
    }
  },
  data: () => ({
    singleDate: new Date().toISOString().substr(0, 10),
    menu: false
  }),
  computed: {
    singleDateFormatted () {
      return moment(this.singleDate).format('DD/MM/YYYY')
    }
  },
  methods: {
    handleChange () {
      this.menu = false
      this.onDateChange(this.singleDateFormatted)
    },
    handleInputChange (inputValue) {
      if(!moment(inputValue).isValid()) {
        alert('Некорректный формат даты')
      } else {
        this.singleDate = moment(inputValue).format('DD/MM/YYYY')
        this.onDateChange(this.singleDate)
      }
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