<template>
<div id="cardio-input-form">
    <form @submit.prevent="handleSubmit">
        <label> Cardio Activity </label>
        <input v-model="item.name" 
        type="text"
        :class="{'has-error' : submitting && invalidItem}"
        @focus="clearStatus"
        />
        <label>Time (minutes)</label>
        <input v-model="item.time" type="number"
        :class="{'has-error' : submitting && invalidItem}"
        @focus="clearStatus"/>
        <label>Distance (miles)</label>
        <input v-model="item.distance" type="number"
        :class="{'has-error' : submitting && invalidItem}"
        @focus="clearStatus"/>
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
            },
            submitting: false, //if any are true in template, render accordingly
            error: false,
            success: false
        }
    },
    methods: {
        handleSubmit() {
            console.log('submitting');
            this.submitting = true;
            this.clearStatus()
            if(this.invalidItem || this.invalidTime) {
                this.error = true;
                return
            }
            this.$emit('add:item', this.item);

            this.item = {
                name: '',
                time: ''
            }

            this.error = false;
            this.success = true;
            this.submitting = false;
        },
        clearStatus() {
            this.success = false
            this.error = false
        }
    },
    computed: {
        invalidItem() {
            return this.item.name === ''
        },
        invalidTime() {
            return this.item.time === ''
        }
    }

}
</script>

<style>
#cardio-input-form {
    display: grid;
    flex-direction: column;
    justify-content: center;
    margin-bottom: 5%;

}
</style>