<template>
  <Header />

  <Form @submit-post="addPost" />
  <div v-if="posts.length === 0">
    <p>Inga inlägg tillgängliga ännu.</p>
  </div>
  <div
    v-else
    class="grid p-2 w-full md:grid-cols-2 xl:grid-cols-3 md:gap-4 md:px-12"
  >
    <Card v-for="(post, index) in posts" :key="index" :post="post" />
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import Form from "./components/Form.vue";
import Header from "./components/Header.vue";

export default {
  name: "App",
  components: {
    Form,
    Card,
    Header,
  },
  data() {
    return {
      posts: JSON.parse(localStorage.getItem("posts")) || [],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost); // Lägg till det nya inlägget i posts-arrayen
      const exists = this.posts.some((post) => post.id === newPost.id); // Kontrollera om inlägget redan finns i arrayen genom att jämföra ID:n
      // Om inlägget inte redan finns i arrayen
      if (!exists) {
        localStorage.setItem("posts", JSON.stringify(this.posts)); // Spara den uppdaterade posts-arrayen i localStorage
      }
    },
  },
};
</script>

<style>
body {
  background-color: #f5f5f5;
}
</style>
