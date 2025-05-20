<template>
<ul class="task-list">
    <TaskItem
        v-for="(task, index) in tasks"
        :key="index"
        :task="task"
        @delete="deleteTask(index)"
    />
</ul>
</template>

<script setup>
import TaskItem from './TaskItem.vue'

const props = defineProps({
    tasks: Array
})

const emit = defineEmits(['delete-task'])

const deleteTask = (index) => {
    emit('delete-task', index)
}
</script>

<style scoped>
.task-list {
    list-style: none;
    padding: 0;
    margin: 0;
}
</style>
