<script setup>
  import getData from "@/composables/getData";
  import Spinner from "@/components/Spinner.vue";
  import { useRoute, useRouter } from "vue-router";

  const props = defineProps({
    id: String
  })
  const route = useRoute();
  const router = useRouter();
  const { fetchedData: post, error, loading, fetchDataWithID, deleteData } = getData(`posts`, route.params.id);

  const handleDelete = async () => {
    await deleteData()
    router.push({ name: "Home" });
  }

  fetchDataWithID();

</script>

<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="post" class="post">
    <h3>{{ post.title }}</h3>
    <p class="pre">{{ post.body }}</p>
    <div class="btn-container">
      <button @click="handleDelete" class="delete">Delete</button>
      <router-link :to="{name: 'Edit', params:{id: post.id} }">
        <button>Edit</button>
      </router-link>
    </div>
  </div>
  <div v-if="loading">
    <Spinner />
  </div>
</template>

<style scoped>
  .post {
    max-width: 1200px;
    margin: 0 auto;
  }
  .post p {
    color: #444;
    line-height: 1.5em;
    margin-top: 40px;
  }
  .pre {
    white-space: pre-wrap;
  }
  .btn-container {
    display: flex;
    justify-content: center;
    gap: 1rem;
  }
</style>
