<template>
  <div
    class="border my-2 bg-[#fafafa] h-auto text-[#8d818c] rounded w-full p-2 shadow-md"
  >
    <div>
      <img
        v-if="post.imageUrl"
        :src="post.imageUrl"
        alt="Image"
        class="w-full h-96 object-cover rounded-sm mb-4"
      />
    </div>
    <div></div>
    <div>
      <h3 class="font-bold">{{ post.title }}</h3>
      <hr />
    </div>
    <p line-clamp-3>{{ post.content }}</p>
  </div>
</template>

<script>
export default {
  name: "Card",

  props: {
    post: Object, // Tar emot ett inlägg som prop
  },
};
</script>
