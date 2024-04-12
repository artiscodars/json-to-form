<script setup>
import { defineProps } from "vue";

// Define props to receive the field data, including options and any field elements
const props = defineProps({
  field: Object,
});
</script>

<template>
  <div>
    <label
      v-if="props.field.field_elements.label"
      for="select-{{ props.field.field_elements.id }}"
      class="form-label"
    >
      {{ props.field.field_elements.label }}
    </label>
    <select
      class="form-select"
      :id="'select-' + props.field.field_elements.id"
      :disabled="props.field.field_elements.disabled === 'disabled'"
    >
      <option disabled value="">
        {{ props.field.field_elements.placeholder }}
      </option>
      <option
        v-for="(option, index) in props.field.options"
        :value="index"
        :key="`option-${index}`"
      >
        {{ option }}
      </option>
    </select>
  </div>
</template>
