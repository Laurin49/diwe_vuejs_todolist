<script setup>
import { computed, ref } from "vue";
import { v4 as uuidv4 } from "uuid";
import TodoItemsCategory from "./components/TodoItemsCategory.vue";
import TheAddTodoItemCard from "./components/TheAddTodoItemCard.vue";

const todoItems = ref([
  {
    id: uuidv4(),
    taskName: "First Tode Item",
    description: "Description 1",
    dueDate: "2022-09-09",
    done: false
  },
  {
    id: uuidv4(),
    taskName: "Second Tode Item",
    description: "Description 2",
    dueDate: "2022-09-10",
    done: true
  },
  {
    id: uuidv4(),
    taskName: "Third Tode Item",
    description: "Description 3",
    dueDate: "2022-09-11",
    done: false
  }
]);

const todoItemsNotDone = computed(() => {
  return todoItems.value.filter((item) => !item.done)
});
const todoItemsDone = computed(() => {
  return todoItems.value.filter((item) => item.done)
});
const todoItemsNotDoneCategoryTitle = computed(
  () => `Upcoming - (${todoItemsNotDone.value.length})`
);

const todoItemsDoneCategoryTitle = computed(
  () => `Done - (${todoItemsDone.value.length})`
);
</script>

<template>
  <header class="colored-header"></header>
  <main>
    <h1 class="title">TodoList</h1>
    <TheAddTodoItemCard />
    <TodoItemsCategory :title="todoItemsNotDoneCategoryTitle" :todo-items="todoItemsNotDone"/>
    <TodoItemsCategory :title="todoItemsDoneCategoryTitle" :todo-items="todoItemsDone"/>
  </main>
</template>

<style scoped>
.colored-header {
  min-height: 5vh;
  min-width: 100vw;
  background: var(--background-light);
}
.title {
  font-size: 2rem;
  font-weight: 600;
  color: #fff;
}
@media (min-width: 600px) {
  main {
    padding: 0 20vw;
  }
}
</style>
