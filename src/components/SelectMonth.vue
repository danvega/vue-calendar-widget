<template>
  <div id="month-view">
    <ul>
      <li v-for="month in months" :key="month.month.name + '-' + month.year" @click="selectMonth(month.month.number,month.year)">
        <span class="year">{{month.year}}</span>
        <span class="month">{{month.month.name}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      monthNames: ['January','February','March','April','May','June','July','August','September','October','November','December'],
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear()
    };
  },
  methods: {
    selectMonth(month,year) {
      this.$emit('selectmonth',month, year);
    }
  },
  computed: {
    months() {
      const months = [];
      for (let i = 0; i <= 12; ++i) {
        let currentIndex = (this.currentMonth + i) % 12;
        months.push({
          month: {
            name: this.monthNames[currentIndex],
            number: currentIndex
          },
          year: currentIndex <= this.currentMonth && i != 0 ? this.currentYear + 1 : this.currentYear
        });
      }
      return months;
    }
  }
};
</script>

<style scoped>
#month-view {
  height: 380px;
  overflow: scroll;
}
#month-view ul {
  list-style-type: none;
  overflow: scroll;
}
#month-view li {
  width: 100%;
  background-color: #f4f5f8;
  padding: 10px;
  cursor: pointer;
}
.year {
  color: lightgray;
  padding-left: 10px;
}
.month {
  text-align: center;
  padding-left: 10px;
  font-size: 18px;
  color: #FD9057;
}
#month-view li:hover {
  background-color: #eeeeee;
  
}
</style>
