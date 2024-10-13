<script lang="ts">
import { computed, defineComponent } from "vue";
import type { PropType } from "vue";

export default defineComponent({
  name: "Info",
  props: {
    info: {
      type: Number as PropType<number>,
      required: true,
    },
    calories: {
      type: Number as PropType<number>,
      required: true,
    },
  },
  components: {},
  setup(props) {
    const updatedCalories = computed(() => props.calories);

    return {
      updatedCalories,
    };
  },
});
</script>

<template>
  <span class="tracker__info"> {{ updatedCalories }} / {{ info }} </span>
</template>

<style scoped>
.tracker__info {
  color: #575d75;
  margin-bottom: 5px;
  font-size: 23px;
  font-weight: bold;
}
</style>
