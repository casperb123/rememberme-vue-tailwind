<template>
  <teleport to="body">
    <div
      class="fixed top-0 left-0 h-screen w-full bg-black bg-opacity-75 flex items-center"
      @click.self="$emit('close')"
    >
      <dialog open class="w-80 rounded-md bg-blue-50">
        <header class="flex justify-between mb-4">
          <h2 class="text-lg font-semibold text-gray-700">Add Resource</h2>
          <button
            class="btn-close text-gray-400 hover:text-gray-500"
            @click="$emit('close')"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              width="24"
              height="24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"
              />
            </svg>
          </button>
        </header>
        <form @submit.prevent="submitData" class="flex flex-col gap-y-2">
          <p v-if="errors.length" class="text-red-600">
            <b>Please correct the following error(s):</b>
            <ul>
              <li v-for="error in errors" :key="error">{{ error }}</li>
            </ul>
          </p>

          <section class="flex flex-col">
            <label for="title">Title</label>
            <input
              type="text"
              name="title"
              id="title"
              class="rounded-md bg-blue-50 border-2 border-gray-400 px-2 py-1"
              :class="{'border-red-600': titleError}"
              v-model="title"
            />
          </section>

          <section class="flex flex-col">
            <label for="description">Description</label>
            <textarea
              name="description"
              id="description"
              rows="5"
              class="rounded-md bg-blue-50 border-2 border-gray-400 px-2 py-1"
              :class="{'border-red-600': descriptionError}"
              v-model="description"
            ></textarea>
          </section>

          <section class="flex flex-col">
            <label for="link">Link</label>
            <input
              type="url"
              name="link"
              id="link"
              class="rounded-md bg-blue-50 border-2 border-gray-400 px-2 py-1"
              :class="{'border-red-600': linkError}"
              v-model="link"
            />
          </section>

          <button type="submit" class="btn-primary">Add</button>
        </form>
      </dialog>
    </div>
  </teleport>
</template>

<script>
export default {
  emits: ["close", "add"],
  data() {
    return {
      errors: [],
      title: null,
      description: null,
      link: null,
      titleError: false,
      descriptionError: false,
      linkError: false,
    };
  },
  methods: {
    validateForm() {
      this.errors = [];
      this.titleError = false;
      this.descriptionError = false;
      this.linkError = false;

      if (!this.title) {
        this.errors.push("Title is required.");
        this.titleError = true;
      }
      if (!this.description) {
        this.errors.push("Description is required.");
        this.descriptionError = true;
      }
      if (!this.link) {
        this.errors.push("Link is required.");
        this.linkError = true;
      }

      if (this.errors.length) return false;
      return true;
    },
    submitData() {
      if (this.validateForm()) {
        this.$emit("add", {
          title: enteredTitle,
          description: enteredDescription,
          link: enteredLink,
        });
      }
    },
  },
};
</script>