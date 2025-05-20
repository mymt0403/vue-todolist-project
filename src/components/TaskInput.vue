<template>
<div class="add-task">
    <input
        v-model="newTask"
        @keyup.enter="submit"
        placeholder="Add a task"
    />
    <button @click="submit">追加</button>
</div>
</template>

<script setup>
    import { ref } from 'vue'

    const emit = defineEmits(['add-task'])
    const newTask = ref('')

    const submit = () => {
        const text = newTask.value.trim()
        /** 有効な文字列がある場合に追加 */
        if (text) {
            emit('add-task', text)
            newTask.value = ''
        }
    }
</script>

<style scoped>
.add-task {
    display: flex;
    align-items: center;
    gap: 10px;
    width: 500px;
    box-sizing: border-box;
}

.add-task input {
    flex: 1;
    height: 40px;
    padding: 0 10px;
    font-size: 16px;
    box-sizing: border-box;
}

.add-task button {
    height: 40px;
    padding: 0 16px;
    white-space: nowrap;
    font-size: 16px;
}
</style>
