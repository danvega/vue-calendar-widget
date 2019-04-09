<template>
  <div id="app">
    <!--https://dribbble.com/shots/3714661-Calendar-Widget-->
    <calendar-widget/>
  </div>
</template>

<script>
import CalendarWidget from '@/components/CalendarWidget';

export default {
  name: 'app',
  components: {
    CalendarWidget
  }
}
</script>

<style>
* {
	padding: 0;
	margin: 0;
}
body {
  margin:0px;
  padding:0px;
  background-color: #FD9057;
  min-height: 100vh;
  font-family: sans-serif;
  display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}
</style>
