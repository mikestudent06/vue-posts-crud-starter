<script setup>
import { RouterLink } from "vue-router";
import Post from "@/components/Post.vue";
import { onMounted, reactive } from "vue";
import axios from "axios";

const state = reactive({
  posts: []
});

onMounted(async () => {
  try {
    const response = await axios.get("http://localhost:8080/posts");
    console.log("response", response.data);
    state.posts = await response.data;
  } catch (error) {
    console.log("Error while fetching: ", error);
  }
});
</script>

<template>
  <div class="center-container">
    <h1>All Post</h1>
    <RouterLink :to="`/`" class="btn btn-blue">Go to Home</RouterLink>
    <RouterLink :to="`/posts/add`" class="btn btn-green">Add Post</RouterLink>

    <br />
    <br />
    <table id="posts">
      <tr>
        <th>S.N</th>
        <th>Title</th>
        <th>Action</th>
      </tr>
      <Post v-for="post in state.posts" :key="post.id" :post="post" />
    </table>
  </div>
</template>
