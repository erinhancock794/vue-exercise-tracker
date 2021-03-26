
<template>
  <tbody>

    <tr v-for="item in items" v-bind:key="item.id">
      <td>{{ item.cardio }} dfgasdrfg</td>
     <td>{{ item.newWeights }}</td>

    </tr>
  </tbody>
</template>


<script>
export default {
  name: "workout-component",
  props: {
    items: Array,
  },
};
</script>