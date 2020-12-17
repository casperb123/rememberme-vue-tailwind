<template>
  <li>
    <a :href="link">
      <base-card>
        <header class="flex items-center justify-between">
          <h2 class="font-semibold text-lg text-gray-700">
            {{ title }}
          </h2>
          <button
            class="text-gray-300 hover:text-gray-400 transition-colors"
            @click.prevent="removeResource(id)"
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
        <p class="mt-2 text-gray-500">{{ description }}</p>
      </base-card>
    </a>
  </li>
</template>

<script>
import BaseCard from "./BaseCard.vue";

export default {
  components: {
    BaseCard,
  },
  props: ["id", "title", "description", "link"],
  inject: ["resources", "removeResource"],
};
</script>