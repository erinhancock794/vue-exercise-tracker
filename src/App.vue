<template>
  <div id="app">
    <h1>Exercises</h1>
    <workouts-form @add:item="addItem($event)"/>
    <exercises :items='exercises'/>
    
  </div>
</template>

<script>
import Exercises from "./components/Exercises.vue";
import WorkoutsForm from './components/WorkoutsForm.vue';

export default {
  name: "App",
  components: {
    Exercises,
    WorkoutsForm,
  },
  data() {
    return {
      exercises: [
        {
          id: 1,
          name: 'Run',
          time: '30'
        },
        {
          id: 2,
          name: 'Stretch',
          time: '15'
        },
        ]
      }
  },
  methods: {
    addItem(item){
      const lastId = this.exercises.length > 0
      ? this.exercises[this.exercises.length -1].id
      : 0;

      const id = lastId + 1;
      const newItem = { ...item, id};
      this.exercises = [...this.exercises, newItem]
    }
    }
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
