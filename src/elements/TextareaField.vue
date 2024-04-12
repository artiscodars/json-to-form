<script setup>
import { defineProps, ref, $emit } from "vue";

// Define props to receive the textarea configuration
const props = defineProps({
  field: Object,
});

// Use a ref for the textarea value to make it reactive
const value = ref(props.field.field_elements.value || "");

// Watch for external changes to the value prop and update the local value accordingly
// This step is optional and mostly useful if the textarea's value can change from the outside after initial render

// Function to emit updates when the textarea value changes, allowing for v-model like behavior in the parent
const updateValue = (event) => {
  // Emit an event for the parent component to update the state
  $emit("update:field", {
    ...props.field,
    field_elements: {
      ...props.field.field_elements,
      value: event.target.value,
    },
  });
};
</script>

<template>
  <div>
    <label
      v-if="props.field.field_elements.label"
      :for="'textarea-' + props.field.field_elements.id"
      class="form-label"
    >
      {{ props.field.field_elements.label }}
    </label>
    <textarea
      class="form-control"
      :id="'textarea-' + props.field.field_elements.id"
      :disabled="props.field.field_elements.disabled === 'disabled'"
      :value="value"
      @input="updateValue"
    ></textarea>
  </div>
</template>
