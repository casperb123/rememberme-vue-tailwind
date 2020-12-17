<template>
  <ul>
    <resource
      v-for="res in resources"
      :key="res.id"
      :id="res.id"
      :title="res.title"
      :description="res.description"
      :link="res.link"
    />
  </ul>
</template>

<script>
import Resource from "./Resource.vue";

export default {
  components: {
    Resource,
  },
  inject: ["resources"],
};
</script>