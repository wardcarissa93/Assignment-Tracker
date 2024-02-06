<template>
  <div id="app">
    <header>
      <h1>Assignment Tracker</h1>
    </header>
    <main>
      <AssignmentTracker />
    </main>
    <footer>
      &copy; {{ getCurrentYear }} - Carissa Ward
    </footer>
  </div>
</template>

<script>
import AssignmentTracker from './components/AssignmentTracker.vue';

export default {
  name: 'Assignment Tracker App',
  components: {
    AssignmentTracker,
  },
  computed: {
    getCurrentYear() {
      return new Date().getFullYear();
    }
  }
};
</script>

<style>
html {
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif;
  text-align: center;
  min-width: 600px;
  background-color: #6c91bf;
  color: white;
}

*, *:before, *:after {
  box-sizing: inherit;
  margin: 0 auto;
  width: 100%;
}

body {
  height: 100vh;
}

#app {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 0.5rem;
  height: 100%;
}

</style>