<script setup lang="ts">
const props = defineProps<{
  colour: {
    name: string;
    value: string;
  };
  selected: {
    name: string;
    value: string;
  };
}>();
</script>

<template>
  <div class="swatch" :style="{ background: props.colour.value }">
    <svg
      v-if="props.colour.value === props.selected.value"
      role="presentation"
      viewBox="0 0 24 24"
      class=""
    >
      <path
        fill="#fff"
        fill-rule="evenodd"
        d="M7.697 13.39a1 1 0 1 1 1.414-1.415l2.12 2.12 4.244-4.241a1 1 0 0 1 1.414 1.414l-4.938 4.937a1 1 0 0 1-1.426.012L7.697 13.39z"
      ></path>
    </svg>
  </div>
</template>

<style scoped lang="postcss">
.swatch {
  height: 36px;
  width: 36px;
  aspect-ratio: 1;

  border-radius: 5px;
  border: solid 1px #dbdde2;

  cursor: pointer;

  &:hover {
    box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.4);
  }

  svg {
    filter: drop-shadow(0 0 2px rgba(0, 0, 0, 0.5));
  }
}
</style>