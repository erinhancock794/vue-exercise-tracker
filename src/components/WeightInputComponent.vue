<template>
<div id="weight-input-form">
    <form @submit.prevent="handleSubmit">
        <label> Activity </label>
        <input v-model="item.name" type="text" :class="{'has-error' : submitting && invalidItem}"
        @focus="clearStatus"/>

        <label>Reps</label>
        <input v-model="item.reps" type="number" :class="{'has-error' : submitting && invalidItem}"
        @focus="clearStatus"/>
        <label>Sets</label>
        <input v-model="item.sets" type="number" :class="{'has-error' : submitting && invalidItem}"
        @focus="clearStatus"/>
        <label>Weight</label>
        <input v-model="item.weight" type="number" :class="{'has-error' : submitting && invalidItem}"
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
                reps: ''
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
                reps: ''
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
#weight-input-form {
    display: grid;
    flex-direction: column;
    justify-content: center;
    margin-bottom: 5%;

}

</style>