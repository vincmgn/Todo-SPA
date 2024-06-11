<template>
  <!-- Container TODO -->
  <VContainer fluid class="d-flex align-center justify-center mt-5">
    <VRow class="d-flex justify-center align-center">
      <VCol cols="12" sm="10" md="8" lg="4" xl="4">
        <!-- Title -->
        <h1 class="text-h3 d-flex justify-center pb-5">CREATE A TODO</h1>
        <!-- Form -->
        <VForm @submit.prevent="addTodo">
          <VTextField
            v-model="input_title"
            label="Title"
            variant="outlined"
            class="mb-4"
          />
          <VTextarea
            v-model="input_description"
            label="Description"
            clear-icon="mdi-close-circle"
            variant="outlined"
            clearable
            class="mb-4"
          />
          <VBtn
            prepend-icon="mdi-plus"
            variant="flat"
            color="teal-darken-2"
            type="submit"
            class="w-100"
          >
            Add a todo
          </VBtn>
        </VForm>
      </VCol>
    </VRow>
  </VContainer>
  <!-- Divider -->
  <VDivider class="mt-5" />
  <!-- List of Todos -->
  <VRow class="d-flex justify-center align-center mt-5">
    <VCol cols="12" sm="10" md="8" lg="4" xl="4">
      <!-- Title -->
      <h1 class="text-h4 d-flex justify-center mb-5">LIST OF TODOS</h1>
      <!-- Check if there are no todos -->
      <div v-if="todos.length === 0" class="text-center">
        Pas encore de todo ajouté
      </div>
      <!-- Cards -->
      <VCard v-for="todo in todos" :key="todo.id" class="mb-5 mx-2 pa-2">
        <VCardItem>
          <!-- Title and Description -->
          <VTextField
            v-model="todo.title"
            label="Title"
            variant="outlined"
            class="pt-2"
            @input="updateTodoTimestamp(todo)"
          />
          <VTextarea
            v-model="todo.description"
            label="Description"
            clear-icon="mdi-close-circle"
            variant="outlined"
            clearable
            hide-details
            @input="updateTodoTimestamp(todo)"
          />
          <p class="text-caption mt-5 text-center teal--text font-weight-bold">
            Updated at: {{ formatDate(todo.updated_at) }}
          </p>
        </VCardItem>
        <div class="pa-4">
          <VDivider></VDivider>
        </div>
        <VCol cols="12" class="d-flex justify-space-around align-center pa-0">
          <!-- Actions -->
          <VCardActions class="d-flex justify-center align-center pa-0 w-100">
            <!-- Delete Button -->
            <VBtn
              prepend-icon="mdi-delete"
              color="red-darken-4"
              variant="tonal"
              @click="deleteTodo(todo)"
              class="mr-5"
            >
              Delete
            </VBtn>
            <!-- Done Button -->
            <VBtn
              prepend-icon="mdi-check"
              :color="todo.done ? 'green' : 'grey'"
              variant="tonal"
              @click="toggleDone(todo)"
              class="ml-5"
            >
              {{ todo.done ? "Done" : "Not Done" }}
            </VBtn>
          </VCardActions>
          <!-- Created At -->
        </VCol>
      </VCard>
    </VCol>
  </VRow>
  <!-- List of Todos -->
</template>

<script setup>
// IMPORTS
import { onMounted, ref, watch } from "vue";
import {
  VContainer,
  VRow,
  VCol,
  VForm,
  VTextField,
  VTextarea,
  VBtn,
  VCard,
  VCardItem,
  VCardActions,
  VDivider,
} from "vuetify/components";

import { format } from "date-fns";

// DATA
const input_title = ref("");
const input_description = ref("");
const todos = ref([]);

// METHODS

// -- add new todo
const addTodo = () => {
  // check if input fields are empty
  if (
    input_title.value.trim() === "" ||
    input_description.value.trim() === ""
  ) {
    return;
  }

  // add new todo to the list
  todos.value.push({
    title: input_title.value,
    description: input_description.value,
    done: false,
    updated_at: new Date().getTime(),
  });

  // clear input fields
  input_title.value = "";
  input_description.value = "";
};

// -- delete todo
const deleteTodo = (todo) => {
  todos.value = todos.value.filter((t) => t.id !== todo.id); // if t is not equal to todo, keep it
};

// -- format date
const formatDate = (timestamp) => {
  return format(new Date(timestamp), "dd/MM/yyyy hh:mm:ss a");
};

// -- update todo timestamp
const updateTodoTimestamp = (todo) => {
  todo.updated_at = new Date().getTime();
};
// -- toggle done
const toggleDone = (todo) => {
  todo.done = !todo.done;
  updateTodoTimestamp(todo);
};

// -- on todo change, save to local storage
watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  { deep: true } // watch entire array (all elements)
);

// -- on component mount, get todos from local storage
onMounted(() => {
  // get todos from local storage
  const storedTodos = JSON.parse(localStorage.getItem("todos")) || [];
  todos.value = storedTodos;
});
</script>

<style scoped></style>
