<template>
  <div id="calendar-widget">
    <calendar-view 
      v-if="showCalendar" 
      :currentMonth="currentMonth"
      :currentYear="currentYear"
      @showmonths="showMonths"
      @selectday="selectDate"
    />
    <select-month 
      v-if="!showCalendar" 
      @selectmonth="selectMonth"
    />
    <p class="selected-date" v-if="selectedDate">Selected Date: {{selectedDate}}</p>
  </div>
</template>

<script>
import CalendarView from '@/components/CalendarView';
import SelectMonth from '@/components/SelectMonth';

export default {
  name: "calendar-widget",
  components: {
    CalendarView,
    SelectMonth
  },
  data() {
    return {
      showCalendar: true,
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      selectedDate: null,
      months: ['January','February','March','April','May','June','July','August','September','October','November','December']
    };
  },
  methods: {
    showMonths() {
      this.showCalendar = false;
    },
    selectMonth(month,year) {
      this.showCalendar = true;
      this.currentMonth = month;
      this.currentYear = year;
    },
    selectDate(day) {
      this.selectedDate = this.months[this.currentMonth] + ' ' + day  + ', ' + this.currentYear;
    }
  }
};
</script>

<style>
#calendar-widget {
  width: 400px;
  height: 380px;
  background-color: #fff;
  border-radius: 5px;
}
.selected-date {
  color: #fff;
  padding:10px;
  text-align: center;
  text-transform: uppercase;
}
</style>
