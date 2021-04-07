
<template>
  <v-container grid-list-md>
    <v-layout row wrap>


      <v-flex xs12 lg2>
        <v-menu
          v-model="menu2"
          :close-on-content-click="false"
          :nudge-right="40"
          lazy
          transition="scale-transition"
          offset-y
          full-width
          max-width="300px"
          min-width="300px"
        >
          <template v-slot:activator="{ on }">
            <v-text-field
              v-model="computedDateFormatted"
              
              label="Date"
              hint="DD//YYYY format"
              persistent-hint
              prepend-icon="event"
              readonly
              color="grey darken-4"
              v-on="on"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date"    :weekday-format="getDay" @input="menu2 = false" color="grey darken-4" :min = dateMin  :allowed-dates="allowedDates(0)" locale="ru-RU"></v-date-picker>
          
        </v-menu>


        
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  import moment from 'moment'

  export default {
    data: vm => ({
      date: new Date().toISOString().substr(0, 10),
      dateMin: new Date().toISOString().substr(0, 10),
      dateFormatted: vm.formatDate(new Date().toISOString().substr(0, 10)),
      menu2: false,
      moment: moment,
      availableDates: [],
      daysOfWeek: ['Вс', 'Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб']
  
      
    }),

    computed: {
      computedDateFormatted () {
        return this.formatDate(this.date)
      }
    },

    

    methods: {
      formatDate (date) {
        if (!date) return null

        const [year, month, day] = date.split('-')
        return `${day}/${month}/${year}`
      },
      parseDate (date) {
        if (!date) return null

        const [day, month, year] = date.split('/')
        return `${year}-${month.padStart(2, '0')}-${day.padStart(2, '0')}`
      },




      allowedDates: function(a){
        return val => ![a].includes(new Date(val).getDay());

      },

      getDay(date){
        let i = new Date(date).getDay(date)
        return this.daysOfWeek[i]
    }


      
    
  },







    }


     
  
</script>



<style lang="scss">
  .v-input__prepend-outer {
    position: absolute;
    left: 215px;
  }
    


</style>