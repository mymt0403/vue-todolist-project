<template>
<li class="task-item">
    <input type="checkbox" v-model="task.completed" />

    <!-- 表示モード -->
    <span
        v-if="!task.editing"
        class="task-text"
        :class="{ completed: task.completed }"
    >
        {{ task.text }}
    </span>

    <!-- 編集モード -->
    <input
        v-else
        ref="editInput"
        class="task-text"
        v-model="task.text"
        @keyup.enter="stopEdit"
        @blur="stopEdit"
        @focus="selectText"
    />

    <!-- 編集ボタン -->
    <EditIcon v-if="!task.editing" @click="startEdit" />

    <!-- 削除ボタン（編集モード中は非表示）-->
    <DeleteIcon v-if="!task.editing" @click="$emit('delete')" />
</li>
</template>

<script setup>
import EditIcon from './icons/IconUpdate.vue'
import DeleteIcon from './icons/IconDelete.vue'
import { ref, nextTick } from 'vue'

const props = defineProps({
    task: Object
})

const editInput = ref(null)
const originalText = ref('')

const startEdit = () => {
    originalText.value = props.task.text
    props.task.editing = true
    nextTick(() => {
        editInput.value?.focus()
    })
}

const stopEdit = () => {
    const trimmed = props.task.text.trim()

    if (trimmed === '') {
        // 空白だけなら元に戻す
        props.task.text = originalText.value
    }

    props.task.editing = false
}

const selectText = () => {
    editInput.value?.select()
}
</script>

<style scoped>
.task-item {
    display: flex;
    align-items: center;
    gap: 10px;
    width: 500px;
    box-sizing: border-box;
    margin: 8px 0;
}

.task-item input[type='checkbox'] {
    width: 20px;
    height: 20px;
    flex-shrink: 0;
}

.task-text {
    flex: 1;
    font-size: 16px;
    padding: 5px 8px;
    box-sizing: border-box;
}

.completed {
    text-decoration: line-through;
    color: gray;
}

.edit-button,
.delete-button {
    height: 32px;
    padding: 4px 10px;
    flex-shrink: 0;
    white-space: nowrap;
    cursor: pointer;
}
</style>
