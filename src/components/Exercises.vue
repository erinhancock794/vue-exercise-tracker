<template>
  <!-- all the html stuff, components html (like the jsx from react) -->
  <div id="exerciseList-table">
    <table>
        <thead>
            <tr>
                <th>Activity</th>
                <th>Time </th>
            </tr>
            <tbody>
                <tr v-for="item in items" :key="item.id">
                    <th>{{item.name}}</th>
                    <th>{{item.time}} minutes</th>
                </tr>
               
            </tbody>
        </thead>
    </table>
  </div>
</template>

<script>
export default {
    name: 'Exercises',
    props: {
        items: Array
    }
};
</script> 

<style scoped>
</style>