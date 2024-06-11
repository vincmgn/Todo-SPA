<template>
  <VApp>
    <Header />
    <VMain>
      <Todo />
    </VMain>
    <Footer />
  </VApp>
</template>

<script setup>
import { VMain, VApp } from "vuetify/components";
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import Todo from "@/components/Todo.vue";
</script>

<style scoped></style>
