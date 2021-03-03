<template>
  <header class="shadow w-screen">
    <nav>
      <nav class="flex items-center justify-between flex-wrap bg-green-400 p-6">
        <div class="flex items-center flex-shrink-0 text-white mr-6">
          <px-icon class="mr-2"></px-icon>
          <router-link to="/" class="font-semibold text-xl tracking-tight">
            PlatziExchange
          </router-link>
        </div>
        <div class="hidden sm:flex flex-grow lg:flex lg:items-center lg:w-auto">
          <div class="text-sm lg:flex-grow">
            <router-link
              v-for="l in menuOptions"
              :key="l.title"
              :to="l.to"
              class="mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:text-white mr-4"
              >{{ l.title }}</router-link
            >
          </div>
        </div>
      </nav>
    </nav>
  </header>
</template>

<script>
import api from "@/api";
import PxIcon from "@/components/PxIcon";

export default {
  name: "PxHeader",

  props: {
    links: {
      type: Array,
      default: () => []
    }
  },

  components: {
    PxIcon
  },

  data() {
    return {
      assets: []
    };
  },

  computed: {
    menuOptions() {
      return this.assets.map(function(asset) {
        return {
          title: asset.symbol,
          to: { name: "coin-detail", params: { id: asset.id } }
        };
      });
    }
  },

  created() {
    api.getAssets(5).then(assets => (this.assets = assets));
  }
};
</script>
