<template>
    <div class="wrapper">
        <div class="app">
            <form
                class="form"
                @submit.prevent="addItem"
            >
                <input
                    class="todo-input"
                    type="text"
                    v-model="text"
                />
                <button type="submit">Add item</button>
            </form>
            <div class="todoItems">
                <ToDoItem
                    v-for="item in todoItems"
                    :key="item.name"
                    :item="item"
                    @toggleTodo="(val) => onToggleTodo(val, item.id)"
                />
            </div>
            <footer
                v-if="todoItems.length"
                class="counters"
            >
                <div>
                    <span>Todo tasks:</span>
                    <strong>{{ todotodoItems }}</strong>
                </div>
                <div>
                    <span>Finished tasks:</span>
                    <strong>{{ finishedtodoItems }}</strong>
                </div>
            </footer>
        </div>
    </div>
</template>

<script setup lang="ts">
    // imports
    import { ref, computed } from "vue";
    import { Item } from "@/types/types";
    import ToDoItem from "./ToDoItem.vue";

    const text = ref("");
    const todoItems = ref<Item[]>([]);

    function addItem() {
        if (!text.value) {
            alert("Field can not be empty!");
            return;
        }

        todoItems.value.push({
            id: Date.now(),
            name: text.value,
            isCompleted: false,
        });
        text.value = "";
    }
    function onToggleTodo(isCompleted, id) {
        const item = todoItems.value.find((i) => i.id === id);
        item.isCompleted = isCompleted;
    }
    const finishedtodoItems = computed(() => {
        return todoItems.value.filter((i) => i.isCompleted).length;
    });
    const todotodoItems = computed(() => {
        return todoItems.value.length - finishedtodoItems.value;
    });
</script>

<style scoped lang="scss">
    .todo-input {
        height: 30px;
        font-size: 20px;
        outline: none;
        padding: 0 5px;
    }
    .counters {
        display: flex;
        justify-content: space-between;
        padding-top: 30px;
    }
    .wrapper {
        display: flex;
        justify-content: center;
    }
    .app {
        max-width: 600px;
        width: 100%;
        padding: 20px;
        background: lightblue;
        border-radius: 5px;
    }
    .form {
        display: flex;
        justify-content: space-between;
        input {
            width: 80%;
        }
        button {
            margin-left: 20px;
            cursor: pointer;
        }
    }
</style>
