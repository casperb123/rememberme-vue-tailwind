<template>
  <div class="container mx-auto">
    <the-header title="Remember Me" />
    <resources />
    <button
      class="w-full rounded-lg border-2 border-dashed border-gray-200 py-5 text-gray-400 hover:border-gray-300 hover:text-gray-500"
      @click="showAddResourceDialog"
    >
      Add Resource
    </button>
  </div>
  <add-resource
    v-if="addResourceDialog"
    @close="hideAddResourceDialog"
    @add="addDialogSubmitted"
  />
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import Resources from "./components/Resources.vue";
import AddResource from "./components/AddResource.vue";

export default {
  components: {
    TheHeader,
    Resources,
    AddResource,
  },
  data() {
    return {
      storedResources: [
        {
          id: "official-guide",
          title: "Official Guide",
          description: "The official Vue.js documentation.",
          link: "https://vuejs.org",
        },
        {
          id: "google",
          title: "Google",
          description: "Learn go google...",
          link: "https://google.com",
        },
      ],
      addResourceDialog: false,
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource,
      showAddResourceDialog: this.showAddResourceDialog,
    };
  },
  methods: {
    addResource(title, description, link) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: link,
      };

      this.storedResources.unshift(newResource);
      this.hideAddResourceDialog();
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
    showAddResourceDialog() {
      this.addResourceDialog = true;
    },
    hideAddResourceDialog() {
      this.addResourceDialog = false;
    },
    addDialogSubmitted(info) {
      this.addResource(info.title, info.description, info.link);
    },
  },
};
</script>