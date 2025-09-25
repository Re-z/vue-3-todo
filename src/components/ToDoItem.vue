<template>
    <div class="todo-item">
        <span
            :class="{ 'is-completed': item.isCompleted }"
            class="todo-text"
        >
            {{ item.name }}
        </span>
        <input
            class="todo-checkbox"
            type="checkbox"
            :value="item.isCompleted"
            @click="toggleItem"
        />
    </div>
</template>

<script setup lang="ts">
    //imports
    import { Item } from "@/types/types";
    import { defineEmits } from "vue";
    const emit = defineEmits(["toggleTodo"]);

    function toggleItem() {
        emit("toggleTodo", !props.item.isCompleted);
    }

    const props = defineProps<{
        item: Item;
    }>();
</script>

<style scoped>
    .todo-checkbox {
        width: 17px;
        height: 17px;
        cursor: pointer;
    }
    .todo-text {
        font-size: 18px;
        padding: 10px 2px 0 10px;
        &.is-completed {
            text-decoration: line-through;
        }

    }
    .todo-item {
        padding: 12px;
        border-bottom: 1px solid #eee;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>
