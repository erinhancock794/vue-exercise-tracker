
<template>
  <tbody>

    <tr v-for="item in items" :key="item.id">
      <td> Cardio {{ item.newCardio }}</td>
     <td> Weights {{ item.newWeights }}</td>

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