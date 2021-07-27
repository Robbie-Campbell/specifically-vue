<template>
    <form @submit="onSubmit" class="add-form p-3 border">
        <div class="d-flex flex-column p-2 border-bottom">
            <label class="mb-2">Task</label>
            <input type="text" v-model="text" name="text" placeholder="Add Task"  class="p-2">
        </div>
        <div class="d-flex flex-column p-2 border-bottom">
            <label class="mb-2">Day and Time</label>
            <input type="text" v-model="day" name="day" placeholder="Add Day and Time"  class="p-2">
        </div>
        <div class="form-control-check d-flex justify-content-between p-2 border-bottom">
            <label>Set Reminder</label>
            <input type="checkbox" v-model="reminder" name="reminder">
        </div>
        <input type="submit"  value="Save Task" class="btn btn-primary w-100">
    </form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
        return {
            text: '',
            day: '',
            reminder: false
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();
            if (!this.text) {
                alert("Please add a task");
                return;
            }

            const newTask = {
                id: Math.floor(Math.random() * 100000),
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }

            this.text = "";
            this.day = "";
            this.reminder = false;

            this.$emit('add-task', newTask);
        }
    }
}
</script>