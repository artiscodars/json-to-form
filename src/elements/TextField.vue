<script setup>
import { ref, watch, defineProps } from "vue";

const props = defineProps({
  field: Object,
});

// If you need to react to changes in your field prop, especially its value, you can use a watch effect
const value = ref(props.field.field_elements.value);

watch(
  () => props.field.field_elements.value,
  (newValue) => {
    value.value = newValue;
  }
);
</script>

<template>
  <div>
    <label
      v-if="props.field.field_elements.label"
      for="input-{{ props.field.field_elements.id }}"
      class="form-label"
    >
      {{ props.field.field_elements.label }}
    </label>
    <input
      type="text"
      class="form-control"
      :id="'input-' + props.field.field_elements.id"
      :value="value"
      @input="
        $emit('update:field', {
          ...props.field,
          field_elements: {
            ...props.field.field_elements,
            value: $event.target.value,
          },
        })
      "
      :disabled="props.field.field_elements.disabled === 'disabled'"
    />
  </div>
</template>
