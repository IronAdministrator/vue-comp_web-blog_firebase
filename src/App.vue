<template>
  <Navbar />
  <router-view :key="route.path"/>
</template>

<script setup>
import Navbar from "@/components/Navbar.vue";
import { useRoute } from "vue-router";

const route = useRoute()

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
