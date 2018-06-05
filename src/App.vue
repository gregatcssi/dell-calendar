<template>
  <div id="app">
    <DellCalendar />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import DellCalendar from './components/DellCalendar.vue';
import Week from './components/week.vue';

@Component({
  components: {
    DellCalendar,Week
  },
})
export default class App extends Vue {}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
