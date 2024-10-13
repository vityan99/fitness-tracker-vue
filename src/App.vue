<script lang="ts">
import { defineComponent } from "vue";

import Tracker from "./components/tracker/Tracker.vue";

export default defineComponent({
  name: "App",
  components: {
    Tracker,
  },
  setup() {
    return {};
  },
});
</script>

<template>
  <div class="container">
    <Tracker
      title="Ходьба"
      :info="1000"
      :percent="50"
      type="walking"
      :stepValue="20"
      :colors="['#24FF00', '#DBFF00', '#FFF500', '#FFB800', '#FF0000']"
    />
  </div>
</template>

<style scoped>
.container {
  display: flex;
  height: 100vh;
  align-items: center;
  justify-content: center;
}
</style>
