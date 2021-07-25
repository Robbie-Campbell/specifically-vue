<template>
    <div class="d-flex justify-content-between mt-3">
        <h1>{{title}}</h1>
        <Button text="Add Task" type="btn-primary"/>
    </div>
</template>

<script>
import Button from './Button.vue';
export default {
    props: {
        title: String
    },
    components: {
        Button,
    }
}
</script>