<template>
  <div class="pages">
    <h1>Pages</h1>
    <nuxt-link
      :to="`/${page.slug}`"
      v-for="page in pages"
      :key="page.id"
      class="list"
    >
      <h3>{{ page.title }}</h3>
    </nuxt-link>
  </div>
</template>

<script setup>
import axios from "axios";

const { data: pages } = await axios.get("http://localhost:4000/pages");
</script>

<style scoped>
.list {
  border: 1px solid;
  margin-bottom: 8px;
  border-radius: 8px;
  padding: 8px;
  cursor: pointer;
  transition: all 0.4s;
  display: block;
  text-decoration: none;
  color: black;
}

.list:hover {
  background-color: cyan;
  border-color: cyan;
}
</style>
