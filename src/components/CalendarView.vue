<template>
  <div id="calendar-view">
    <div id="header">
      <div class="month">{{monthName}}, {{currentYear}}</div>
      <div class="menu">
        <i class="fas fa-bars" @click="showMonths"></i>
      </div>
    </div>
    <div class="week">
      <div v-for="d in daysOfWeek" v-bind:key="d.day" class="week-day">{{ d.abbr }}</div>
    </div>
    <div class="calendar-days">
      <div v-for="day in calendarDays" v-bind:key="day" class="calendar-day">
        <button @click="selectDay(day)" :class="{ active: day == selectedDay }">{{ day }}</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'calendar-view',
  props: {
    currentMonth: {
      type: Number,
      required: true
    },
    currentYear: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      daysOfWeek: [
        { day: 'Sunday', abbr: 'S'},
        { day: 'Monday', abbr: 'M'},
        { day: 'Tuesday', abbr: 'T'},
        { day: 'Wednesday', abbr: 'W'},
        { day: 'Thursday', abbr: 'T'},
        { day: 'Friday', abbr: 'F'},
        { day: 'Saturday', abbr: 'S'}
      ],
      months: ['January','February','March','April','May','June','July','August','September','October','November','December'],
      calendarDays: Array.from(Array(31), (x, index) => index + 1),
      selectedDay: null
    }
  },
  methods: {
    selectDay(day) {
      this.selectedDay = day;
      this.$emit('selectday',day);
    },
    showMonths() {
      this.$emit('showmonths');
    }
  },
  computed: {
    monthName() {
      return this.months[this.currentMonth];
    }
  }
};
</script>

<style>
#calendar-view {
  height: 380px;
}
#header {
  display: flex;
  flex-direction: row;
  background-color: #f4f5f8;
  padding: 20px 10px;
  border-radius: 5px;
}
.month {
  font-size: 21px;
  align-self: flex-start;
}
.menu {
  margin-left: auto;
}
.week {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-gap: 20px;
  background-color: #f4f5f8;
}
.week-day {
  color: #fd9057;
  text-align: center;
  padding:5px;
}
.calendar-days {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-gap: 20px;
}
.calendar-day {
  text-align: center;
  
}
.calendar-day button { 
  border: none;
  background: none;
  cursor: pointer;
  font-size: 15px;
  padding: 10px;
  border-radius: 20px;
  outline: none;
}
.calendar-day button:hover {
  background-color: #fd9057;
  color:#fff;
}
.calendar-day button.active {
  background-color: #fd9057;
  color:#fff;
}
.fa-bars {
  cursor: pointer;
}
</style>
