<script setup>
import { defineProps } from "vue";

// Define props to receive the field data, including any specifics for the date input
const props = defineProps({
  field: Object,
});
</script>

<template>
  <div>
    <label
      v-if="props.field.field_elements.label"
      :for="'date-' + props.field.field_elements.id"
      class="form-label"
    >
      {{ props.field.field_elements.label }}
    </label>
    <input
      type="date"
      class="form-control"
      :id="'date-' + props.field.field_elements.id"
      :value="props.field.field_elements.value"
      :disabled="props.field.field_elements.disabled === 'disabled'"
      @input="
        $emit('update:field', {
          ...props.field,
          field_elements: {
            ...props.field.field_elements,
            value: $event.target.value,
          },
        })
      "
    />
  </div>
</template>
