<script lang="ts">
import { defineComponent } from "vue";
import type { PropType } from "vue";

export default defineComponent({
  name: "Button",
  props: {
    title: {
      type: String as PropType<string>,
      required: true,
    },
    clickHandler: {
      type: Function as PropType<() => void>,
      required: true,
    },
  },
  components: {},
  setups() {
    return {};
  },
});
</script>

<template>
  <button class="btn" @click="clickHandler">{{ title }}</button>
</template>

<style scoped>
.btn {
  cursor: pointer;
  border: 1px solid #ffc94f;
  border-radius: 5px;
  color: #ffc94f;
  background-color: transparent;
  padding: 10px 15px;
}
</style>
