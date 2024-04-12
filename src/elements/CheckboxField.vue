<script setup>
import { defineProps, ref, $emit } from "vue";

// Define props to receive the checkbox configuration
const props = defineProps({
  field: Object,
  index: Number, // Assuming you pass the index to manage unique IDs
});

// Use a ref to make the checked state reactive and controllable
const isChecked = ref(props.field.field_elements.checked === "checked");

// Emit update event when the checkbox state changes
const updateCheckedState = (event) => {
  // Emit an event for the parent component to update the state
  // You might need to adjust the event name and payload according to your needs
  $emit("update:field", {
    ...props.field,
    field_elements: {
      ...props.field.field_elements,
      checked: event.target.checked ? "checked" : "",
    },
  });
};
</script>

<template>
  <div class="form-check">
    <input
      class="form-check-input"
      type="checkbox"
      :id="`checkbox-${index}`"
      :checked="isChecked"
      @change="updateCheckedState"
    />
    <label class="form-check-label" :for="`checkbox-${index}`">
      {{ props.field.field_elements.label }}
    </label>
  </div>
</template>
