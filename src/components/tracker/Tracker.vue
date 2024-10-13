<script lang="ts">
import { defineComponent, onMounted, ref, watch } from "vue";
import type { PropType } from "vue";

import Info from "../info/Info.vue";
import Status from "../status/Status.vue";
import Percent from "../percent/Percent.vue";
import Button from "../button/Button.vue";

export default defineComponent({
  name: "Tracker",
  props: {
    title: {
      type: String as PropType<string>,
      required: true,
    },
    info: {
      type: Number as PropType<number>,
      required: true,
    },
    percent: {
      type: Number as PropType<number>,
      required: true,
    },
    type: {
      type: String as PropType<string>,
      required: true,
    },
    stepValue: {
      type: Number as PropType<number>,
      required: true,
    },
    colors: {
      type: Array as PropType<string[]>,
      required: true,
    },
  },
  components: {
    Info,
    Status,
    Percent,
    Button,
  },
  setup(props) {
    const calories = ref((props.info / 100) * props.percent);
    const actualPercent = ref(parseFloat(((calories.value / props.info) * 100).toFixed(0)));
    const status = ref("");
    const color = ref("");

    const step: number = (props.info / 100) * props.stepValue;

    const calculateStatus = (): void => {
      if (actualPercent.value < 50) {
        status.value = "легкий";
      }

      if (actualPercent.value >= 50 && actualPercent.value < 70) {
        status.value = "средний";
      }

      if (actualPercent.value >= 70) {
        status.value = "сложный";
      }
    };

    const setActualPercent = (): void => {
      actualPercent.value = parseFloat(((calories.value / props.info) * 100).toFixed(0));
    };

    const getActualColor = (): void => {
      if (actualPercent.value >= 0 && actualPercent.value <= 20) {
        color.value = props.colors[0];
      }

      if (actualPercent.value > 20 && actualPercent.value <= 40) {
        color.value = props.colors[1];
      }

      if (actualPercent.value > 40 && actualPercent.value <= 60) {
        color.value = props.colors[2];
      }

      if (actualPercent.value > 60 && actualPercent.value <= 80) {
        color.value = props.colors[3];
      }

      if (actualPercent.value > 80 && actualPercent.value <= 100) {
        color.value = props.colors[4];
      }
    };

    watch(calories, () => {
      setActualPercent();
      calculateStatus();
      getActualColor();
    });

    const decrease = (): void => {
      calories.value = Math.max(calories.value - step, 0);
    };

    const increase = (): void => {
      calories.value = Math.min(calories.value + step, props.info);
    };

    onMounted(() => {
      setActualPercent();
      calculateStatus();
      getActualColor();
    });

    return {
      ...props,
      calories,
      actualPercent,
      status,
      color,
      decrease,
      increase,
    };
  },
});
</script>

<template>
  <div :class="['tracker', `tracker--${type}`]">
    <h2 class="tracker__title">{{ title }}</h2>
    <Info :info="info" :calories="calories" />
    <Status :status="status" />
    <Percent :color="color" :actualPercent="actualPercent" />

    <div class="tracker__controllers">
      <Button title="Убавить" :clickHandler="() => decrease()" />
      <Button title="Прибавить" :clickHandler="() => increase()" />
    </div>
  </div>
</template>

<style scoped>
.tracker {
  display: flex;
  flex-direction: column;
  background-color: #151a30;
  border-radius: 8px;
  width: 190px;
  padding: 10px 20px;
  margin: 0 auto;
  margin-bottom: 20px;
  box-shadow: 4px 4px 16px 3px rgba(34, 60, 80, 0.2);
}

.tracker__title {
  margin: 0;
  margin-bottom: 10px;
}

.tracker__status {
  color: #ffc94f;
  margin-bottom: 5px;
}

.tracker__percent {
  width: 100%;
  height: 30px;
  background-color: #575d75;
  margin-bottom: 10px;
  border-radius: 5px;
}

.tracker__percent-value {
  padding-left: 5px;
  border-radius: 5px;
  height: 30px;
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.tracker--run .tracker__title {
  color: #ffc94f;
}

.tracker--walking .tracker__title {
  color: #42aaff;
}

.tracker--calories .tracker__title {
  color: #2ce49a;
}

.tracker__controllers {
  display: flex;
  gap: 10px;
  align-items: center;
  margin: 0 auto;
}
</style>
