<template>
  <div id="app">
    <h1>Exercises</h1>
    <button v-on:click="toggleSelection">{{ inputMethod }}</button>

    <div v-if="checked">
      <cardio-input-component @add:item="addItem($event)" />
    </div>
    <div v-else>
      <weight-input-component @add:item="addItem($event)" />
    </div>

    <button v-on:click="saveWorkout">Save Workout</button>
    
    <div>
      <cardio-exercises
        :items="cardio"
        @edit:item="editItem"
        @delete:item="deleteItem"
      />
      <weight-exercises
        :items="weights"
        @edit:item="editItem"
        @delete:item="deleteItem"
      />
    </div>
    <div>
      <h3>Workout History</h3>
    <workout-component 
    :workouts="workouts"
    />
    </div>
    
  </div>
</template>

<script>
import CardioExercises from "./components/CardioExercises.vue";
import CardioInputComponent from "./components/CardioInputComponent.vue";
import WeightExercises from "./components/WeightExercises.vue";
import WeightInputComponent from "./components/WeightInputComponent.vue";
import WorkoutComponent from "./components/WorkoutComponent.vue";


export default {
  name: "App",
  components: {
    CardioExercises,
    CardioInputComponent,
    WeightExercises,
    WeightInputComponent,
    WorkoutComponent
  },
  data() {
    //contain all of the data in this function
    return {
      checked: false,
      workoutId: 0,
      cardio: [
        {
          id: 1,
          name: "Run",
          time: "30",
          distance: 3,
          workoutId: 0,
        },
        {
          id: 2,
          name: "Stretch",
          time: "15",
          distance: 4,
          workoutId: 0,
        },
      ],
      weights: [
        {
          id: 1,
          name: "Bench Press",
          reps: 2,
          sets: 3,
          weight: 30,
          workoutId: 0,
        },
      ],
      workouts: [
        {
        id: -1,
        cardio: [],
        weights: []
      }
      ]
    };
  },
  methods: {
    saveWorkout() {
      let newCardio = this.cardio.filter((obj) => obj.workoutId === this.workoutId)
      let newWeights = this.weights.filter((obj) => obj.workoutId === this.workoutId)
      console.log('newCardio-->', newCardio)
      console.log('newWeights--->', newWeights)
      let id = this.workoutId
      let newItem = { id, newCardio, newWeights }
      console.log('newItem-', newItem);
      this.workouts = [...this.workouts, newItem]
      this.cardio = []
      this.weights = []
      this.workoutId += 1
      console.log('this.workouts---->', this.workouts)
    },
    addItem(item) {
      let lastId;
      let id;
      let newItem;
      if (item.time) {
        lastId =
          this.cardio.length > 0 ? this.cardio[this.cardio.length - 1].id : 0;

        id = lastId + 1;
        newItem = { ...item, id };
        newItem.workoutId = this.workoutId;
        this.cardio = [...this.cardio, newItem];
      } else {
        lastId =
          this.weights.length > 0 ? this.cardio[this.cardio.length - 1].id : 0;

        id = lastId + 1;
        newItem = { ...item, id };
        this.weights = [...this.weights, newItem];
      }
    },
    deleteItem(item) {
      if (item.time) {
        this.cardio = this.cardio.filter((object) => item.id !== object.id);
      } else {
        this.weights = this.weights.filter((object) => item.id !== object.id);
      }
    },
    editItem(id, updatedItem) {
      console.log("id---->", id);
      if (updatedItem.time) {
        this.cardio = this.cardio.map((item) =>
          item.id === id ? updatedItem : item
        );
      } else {
        this.weights = this.weights.map((item) =>
          item.id === id ? updatedItem : item
        );
      }
    },
    toggleSelection() {
      this.checked = !this.checked;
    },
  },
  computed: {
    inputMethod: function () {
      return this.checked ? "Cardio" : "Strength";
    },
    savedWorkouts: function () {
      return this.workouts.filter(workout => workout.id)
    }
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
