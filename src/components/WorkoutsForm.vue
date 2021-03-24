<template>
<div id="workouts-form">
    <form @submit.prevent="handleSubmit">
        <label> Workout Activity </label>
        <input v-model="item.name" type="text"/>
        <label>Duration</label>
        <input v-model="item.time" type="number"/>
        <button>Add</button>
    </form>
</div>
  
</template>

<script>
export default {
    name: 'workouts-form',
    data() {
        return {
            item: {
                name: '',
                time: ''
            }
        }
    },
    methods: {
        handleSubmit() {
            this.$emit('add:item', this.item);
            console.log('submitting');
        }
    }

}
</script>

<style>

</style>