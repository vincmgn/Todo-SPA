<template>
  <!-- Container TODO -->
  <VContainer fluid class="d-flex align-center justify-center fill-height">
    <VRow class="d-flex justify-center align-center">
      <VCol cols="12" sm="10" md="8" lg="4" xl="2">
        <!-- Title -->
        <h1 class="d-flex justify-center pb-5">CREATE A TODO</h1>
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
</template>

<script setup>
import { ref } from "vue";
import {
  VContainer,
  VRow,
  VCol,
  VForm,
  VTextField,
  VTextarea,
  VBtn,
} from "vuetify/components";

// DATA
const input_title = ref("");
const input_description = ref("");

// METHODS
const addTodo = () => {
  // check if input fields are empty
  if (
    input_title.value.trim() === "" ||
    input_description.value.trim() === ""
  ) {
    return;
  }
  console.log(input_title.value, input_description.value);
};
</script>

<style scoped>
.fill-height {
  height: 100vh;
}
</style>
