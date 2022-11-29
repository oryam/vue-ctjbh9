<template>
  <div id="app">
    <ProfileRadarChart />
    <ProfileAtomicChart />
  </div>
</template>

<script>
import ProfileAtomicChart from './components/ProfileAtomicChart.vue';
import ProfileRadarChart from './components/ProfileRadarChart.vue';

export default {
  name: 'App',
  components: {
    ProfileAtomicChart,
    ProfileRadarChart,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
