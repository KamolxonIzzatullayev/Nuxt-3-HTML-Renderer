<template>
  <div>
    <div v-html="page.content"></div>
    <div class="button">
      <nuxt-link to="/">Back to Pages</nuxt-link>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const page = ref({});

const route = useRoute();

onMounted(async () => {
  const res = await axios.get(`http://localhost:4000/pages`);
  let currentId = null;
  res.data.forEach((element) => {
    if (element.slug == route.params.id) {
      currentId = element.id;
    }
  });

  const response = await axios.get(`http://localhost:4000/pages/${currentId}`);
  page.value = response.data;

  useHead({
    title: page.value.title,
    meta: [{ name: "keywords", content: page.value.keywords }],
  });
});
</script>

<style scoped>
.button {
  padding: 8px 0;
  text-align: right;
}

.button a {
  text-decoration: none;
  display: inline-block;
  background-color: rgb(68, 68, 255);
  color: white;
  padding: 8px 16px;
  border-radius: 8px;
}
</style>
