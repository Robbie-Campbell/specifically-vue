<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" class="mt-3 bg-light p-3" :class="[task.reminder ? 'reminder' : '', 'task']">
        <h1 class="d-flex justify-content-between">
            <span>{{task.text}}</span>
            <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
        </h1>
        <p class="text-muted">{{task.day}}</p>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object
    },
    methods: {
        onDelete(id) {
            this.$emit('delete-task', id);
        }
    },
    emits: ['delete-task', 'toggle-reminder'],
}
</script>

<style scoped>
.fas {
    color: red;
}

.reminder {
    border-left: 5px solid green;
}
</style>