<script setup>
import { ref } from 'vue';


const newTodo = ref('');

const nextId = ref(2)
const handleSubmit = () => {
  if(newTodo.value.trim()) {
    emit('add-todo', {id : nextId.value++, text: newTodo.value, completed: false, editing: false});
    newTodo.value = '';
  }
}

const emit = defineEmits([['add-todo']]);

</script>

<template>
    <div>
      <form @submit.prevent="handleSubmit" class="d-flex justify-content-center align-items-center mb-4">
              <div  class="form-outline flex-fill">
                <input v-model="newTodo" type="text" id="form2" class="form-control" placeholder="Add a todo" />
              </div>
              <button type="submit"  class="btn btn-info ms-2">Add</button>
            </form>
    </div>
</template>

<style scoped>

</style>
