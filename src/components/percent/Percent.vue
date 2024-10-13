<script lang="ts">
import { computed, defineComponent, onMounted } from "vue";
import type { PropType } from "vue";

export default defineComponent({
  name: "Percent",
  props: {
    actualPercent: {
      type: Number as PropType<number>,
      required: true,
    },
    color: {
      type: String as PropType<string>,
      required: true,
    },
  },
  components: {},
  setup(props) {
    const updatedColor = computed(() => props.color);
    const updatedActualPercent = computed(() => props.actualPercent);

    const percentComponentStyle = computed(() => {
      return { backgroundColor: updatedColor.value, width: `${updatedActualPercent.value}%` };
    });

    return { updatedColor, updatedActualPercent, percentComponentStyle };
  },
});
</script>

<template>
  <div class="tracker__percent">
    <div class="tracker__percent-value" :style="percentComponentStyle">{{ updatedActualPercent }}%</div>
  </div>
</template>

<style scoped>
.tracker__percent {
  width: 100%;
  height: 30px;
  background-color: #575d75;
  margin-bottom: 10px;
  border-radius: 5px;
  overflow: hidden;
}

.tracker__percent-value {
  padding-left: 5px;
  border-radius: 5px;
  height: 30px;
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  white-space: nowrap;
}
</style>
