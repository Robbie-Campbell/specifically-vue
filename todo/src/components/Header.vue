<template>
    <div class="d-flex justify-content-between mt-3">
        <h1>{{title}}</h1>
        <Button @toggle-add-task="$emit('toggle-add-task')" 
        :text="showAddTask ? 'Close' : 'Add Task'" 
        :type="showAddTask ? 'btn-danger' : 'btn-primary'"/>
    </div>
</template>

<script>
import Button from './Button.vue';
export default {
    props: {
        title: String,
        showAddTask: Boolean
    },
    components: {
        Button,
    }
}
</script>