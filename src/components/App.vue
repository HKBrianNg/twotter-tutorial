<template>
  <div id="app">
    <UserProfile />
  </div>
</template>

<script>
import UserProfile from './UserProfile.vue';

export default {
  name: 'App',
  components: {
    UserProfile
  },
}
</script>

<style>
#app {
  margin: 0px;
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; */
  /* text-align: center; */
  /* color: #2c3e50; */
  /* margin-top: 20px;
  display:flex;
  flex-direction: column; */
}
</style>
