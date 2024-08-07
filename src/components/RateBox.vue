<template>
  <div class="rate-box">
    <StarIcon
      v-for="index in 5"
      :key="index"
      :class="{
        filled: index <= (hoverValue || value),
        clickable: !editable,
      }"
      @mouseover="editable ? onMouseOver(index) : null"
      @mouseleave="editable ? onMouseLeave() : null"
      @click="editable ? onClick(index) : null"
    />
  </div>
</template>

<script>
import { ref, watch } from "vue";
import StarIcon from "./StarIcon.vue";

export default {
  name: "RateBox",
  components: {
    StarIcon,
  },
  props: {
    modelValue: {
      type: Number,
      default: 0,
    },
    editable: {
      type: Boolean,
      default: false,
    },
  },
  emits: ["update:modelValue"],
  setup(props, { emit }) {
    const value = ref(props.modelValue);
    const hoverValue = ref(null);

    watch(
      () => props.modelValue,
      (newValue) => {
        value.value = newValue;
      }
    );

    const onMouseOver = (index) => {
      hoverValue.value = index;
    };

    const onMouseLeave = () => {
      hoverValue.value = null;
    };

    const onClick = (index) => {
      if (value.value === index) {
        emit("update:modelValue", 0);
        hoverValue.value = null;
      } else {
        emit("update:modelValue", index);
      }
    };

    return {
      value,
      hoverValue,
      onMouseOver,
      onMouseLeave,
      onClick,
    };
  },
};
</script>

<style>
.rate-box {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
}

svg {
  cursor: pointer;
  fill: #333; /* Boş durum için renk */
  width: 2rem;
  height: 2rem;
}

svg.filled {
  fill: gold; /* Doldurulmuş yıldızlar için renk */
}

svg.clickable {
  cursor: auto;
}
</style>
