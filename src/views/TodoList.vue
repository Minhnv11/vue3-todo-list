<script setup>
import { computed, ref } from 'vue';
import AddTodo from './AddTodo.vue'
import TabTodo from './TabTodo.vue'
import TabTodoContent from './TabTodoContent.vue'


// Todo List 
const todoLists = ref([
  {id:1, text: 'task 1', completed: false, editing: false},
]);

// TabTodo 
const tabs = ref([
  {id:1, name: 'All'},
  {id:2, name: 'Active'},
  {id:3, name: 'Completed'},
])

const selectedTab = ref('All')
const selectTab = (tab) => {
  selectedTab.value = tab;
  console.log(selectedTab.value);
}

const filteredTodos = computed(() => {
  if(selectedTab.value === 'All') {
    return todoLists.value;
  } else if(selectedTab.value === 'Active') {
    return todoLists.value.filter(todo => !todo.completed);
  } else if(selectedTab.value === 'Completed') {
    return todoLists.value.filter(todo => todo.completed);
  }

})

// Add todo 
const addTodo = (todo) => {
  todoLists.value.push(todo);
}
// 
const saveEdit  = (todo)  => {
  // console.log(todo);
 const index = todoLists.value.findIndex(t => t.id === todo.id);
 todoLists.value[index] = todo;
 todo.editing = false;

}
// delete todo 
const removeTodo = (id) => {
  todoLists.value = todoLists.value.filter(todo => todo.id !== id);
}
</script>

<template>
 <section class="vh-100 gradient-custom">
  <div class="container py-5 h-100">
    <div class="row d-flex justify-content-center align-items-center h-100">
      <div class="col col-xl-10">
        <div class="card">
          <div class="card-body p-5">
            <AddTodo @add-todo="addTodo" />
            <TabTodo  @select-tab="selectTab" :tabs="tabs" :selectedTab="selectedTab"/>
            <TabTodoContent @remove-todo="removeTodo" @save-edit="saveEdit" :todoLists="filteredTodos"  />
          </div>
        </div>

      </div>
    </div>
  </div>
</section>
</template>

<style scoped>

</style>
