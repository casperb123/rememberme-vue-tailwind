<template>
  <header class="flex justify-between py-5 items-center mb-5">
    <h1 class="uppercase text-gray-500">{{ title }}</h1>
    <button class="btn-primary" @click="showAddResourceDialog">
      <svg
        class="mr-2"
        xmlns="http://www.w3.org/2000/svg"
        width="12"
        height="12"
        viewBox="0 0 24 24"
        fill="currentColor"
      >
        <path d="M24 10h-10v-10h-4v10h-10v4h10v10h4v-10h10z" />
      </svg>
      Add
    </button>
  </header>
</template>

<script>
export default {
  props: ["title"],
  inject: ["showAddResourceDialog"],
};
</script>