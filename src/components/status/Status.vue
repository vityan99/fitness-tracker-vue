<script lang="ts">
import { computed, defineComponent } from "vue";
import type { PropType } from "vue";

export default defineComponent({
  name: "Status",
  props: {
    status: {
      type: String as PropType<string>,
      required: true,
    },
  },
  components: {},
  setup(props) {
    const updatedStatus = computed(() => props.status);

    return {
      updatedStatus,
    };
  },
});
</script>

<template>
  <span class="tracker__status">Уровень: {{ updatedStatus }}</span>
</template>

<style scoped>
.tracker__status {
  color: #ffc94f;
  margin-bottom: 5px;
}
</style>
