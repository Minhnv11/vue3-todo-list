<script setup>
const props = defineProps({
  todoLists: Array,
});
const emit = defineEmits(['remove-todo', 'save-edit']);

// delete todo

const removeTodo = (id) => {
   emit('remove-todo', id)
  //  console.log('delete', id)
}
//
const saveEdit = (todo) => {
  emit('save-edit', todo)
  // console.log(todo)
}
</script>

<template>
        <!-- Tabs content -->
        <div class="tab-content ">
                <div v-for="todo in todoLists" :key="todoLists.id" class="d-flex bd-highlight p-1 mb-2" style="background-color: #f4f6f7;">
                    <div  class="p-2 flex-grow-1 bd-highlight" > 
                      <input v-if="!todo.editing" v-model="todo.completed" class="form-check-input " type="checkbox" value="" />
                      <span v-if="!todo.editing" :class="{completed: todo.completed}" class="ms-3"> {{ todo.text }} </span>
                      <input  v-else class="form-control " v-model="todo.text"ype="text">
                    </div>
                    <div v-if="todo.editing" @click="saveEdit(todo)" class="bd-highlight me-3"> <button @click="todo.editing = true" class="btn btn-outline-success"><span><i class="bi bi-floppy-fill"></i></span></button></div>
                    <div v-else class="bd-highlight me-3"> <button @click="todo.editing = true" class="btn btn-outline-success"><span><i class="bi bi-pencil-square"></i></span></button></div>
                    <div class="bd-highlight"> <button @click="removeTodo(todo.id)" class="btn btn-outline-danger"><span><i class="bi bi-trash"></i></span></button> </div>
                </div>
        </div>
        <!-- Tabs content -->
</template>

<style scoped>
.completed {
    text-decoration: line-through;
    color: red;
}
</style>
