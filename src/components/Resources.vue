<template>
  <transition-group tag="ul" name="list" class="relative">
    <resource
      v-for="res in resources"
      :key="res.id"
      :id="res.id"
      :title="res.title"
      :description="res.description"
      :link="res.link"
    />
  </transition-group>
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

<style scoped>
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-leave-active {
  position: absolute;
  width: 100%;
}

.list-enter-from {
  opacity: 0;
  transform: translateX(-50px);
}

.list-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.list-leave-to {
  opacity: 0;
  transform: translateX(50px);
}

.list-move {
  transition: transform 0.5s ease;
}
</style>