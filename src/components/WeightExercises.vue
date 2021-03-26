<template>
  <!-- all the html stuff, components html (like the jsx from react) -->
  <div id="weightsList-table">

    <table class="striped-table">
        <thead>
            <tr>
                <th>Weights Activity</th>
                <th>Reps </th>
                <th> Sets </th>
                <th> Weight </th>
            </tr>
            <tbody>
                <tr v-for="item in items" :key="item.id">
                    <td v-if="editing === item.id">
                        <input v-model="item.name" type="text" ></td>
                    <td v-else>{{item.name}}</td>

                    <td>{{item.reps}}</td>
                    <td>{{item.sets}}</td>
                    <td>{{item.weight}}</td>


                    <td v-if="editing === item.id">
                        <button @click="editItem(item)">Save</button>
                        <button @click="cancelEdit(item)"> Cancel</button>
                    </td>
                    <td v-else>
                        <button @click="editMode(item)">Edit</button>
                        <button @click="deleteItem(item)"> Delete</button>
                    </td>
                </tr>
               
            </tbody>
        </thead>
    </table>
  </div>
</template>

<script>
export default {
    name: 'WeightExercises',
    props: {
        items: Array
    },
    data(){
        return {
            editing: null,
            cachedItem: null
        }
    },
    methods: {
        editMode(item) {
            this.cachedItem = Object.assign({}, item)
            this.editing = item.id;
        },
        editItem(item) {
            if (item.name === '' || item.amount === '') return

            this.$emit('edit:item', item.id, item)
            this.editing = null;
        },
        deleteItem(item) {
            this.$emit('delete:item', item)
        },
        cancelEdit(item) {
            Object.assign(item, this.cachedItem)
            this.editing = null;
        }

    }
    // emits: ['delete:item']
};
</script> 

<style scoped>
table {
    display: flex;
    justify-content: center;
}
button {
    margin-right: 5px;
}
</style>