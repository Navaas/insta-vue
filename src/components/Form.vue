<template>
  <div class="flex justify-center items-center md:mt-12 p-2">
    <div
      class="bg-[#f5f5f5] p-4 text-black shadow-lg rounded-md w-full md:w-1/2 xl:w-1/4"
    >
      <!-- Form start -->
      <form action="" class="flex flex-col" @submit="submitForm">
        <!-- Titel -->
        <label for="title" class="text-[#8d818c] font-bold">Titel</label>
        <input
          type="text"
          id="title"
          v-model="formData.title"
          placeholder="Lägg till titel.."
          class="p-2 rounded-md text-[#8d818c] border border-gray-300"
        />
        <!-- Beskrivning -->
        <label for="content" class="text-[#8d818c] font-bold"
          >Beskrivning</label
        >
        <textarea
          name="content"
          id="content"
          v-model="formData.content"
          class="p-2 rounded-md border border-gray-300 text-[#8d818c]"
          placeholder="Lägg till beskrivning.."
        ></textarea>
        <!-- Bild url -->
        <label for="imageUrl" class="text-[#8d818c] font-bold">Bild url</label>
        <input
          type="text"
          id="imageUrl"
          v-model="formData.imageUrl"
          placeholder="Skriv in bildens URL"
          class="url-input p-2 rounded-md text-[#8d818c]border border-gray-300"
        />
        <!-- Knapp -->
        <button class="bg-[#8d818c] p-2 w-1/4 text-white mt-2 rounded-md">
          Skicka
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      // Data för formuläret
      formData: {
        title: "",
        content: "",
        imageUrl: "",
      },
      posts: [],
    };
  },
  methods: {
    submitForm(event) {
      event.preventDefault();
      //   Skickar data till föräldern (App.vue)
      this.$emit("submit-post", { ...this.formData });

      // Hämta befintliga inlägg från localStorage
      const existingPosts = JSON.parse(localStorage.getItem("posts")) || [];

      // Lägg till det nya inlägget
      existingPosts.push({ ...this.formData });

      // Spara tillbaka inläggen i localStorage
      localStorage.setItem("posts", JSON.stringify(existingPosts));

      // Uppdatera den lokala posts arrayen för att visa nya inlägget
      this.posts = existingPosts;

      // Rensa formuläret efter att inlägget sparats
      this.formData.title = "";
      this.formData.content = "";
      this.formData.imageUrl = "";
    },
  },
};
</script>

<style scoped></style>
