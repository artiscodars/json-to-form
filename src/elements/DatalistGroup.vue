<script setup>
import { defineProps } from "vue";

// Define props to receive the field configuration, including options and any field elements
const props = defineProps({
  field: Object,
});
</script>

<template>
  <div>
    <label
      v-if="props.field.field_elements.label"
      :for="'datalist-' + props.field.field_elements.id"
      class="form-label"
    >
      {{ props.field.field_elements.label }}
    </label>
    <input
      class="form-control"
      :list="'datalist-options-' + props.field.field_elements.id"
      :placeholder="props.field.field_elements.placeholder"
      :id="'datalist-' + props.field.field_elements.id"
    />
    <datalist :id="'datalist-options-' + props.field.field_elements.id">
      <option
        v-for="(option, index) in props.field.options"
        :value="option"
        :key="`option-${index}`"
      >
        {{ option }}
      </option>
    </datalist>
  </div>
</template>
