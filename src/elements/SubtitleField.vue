<script setup>
import { defineProps } from "vue";

// Define props to receive the field data
const props = defineProps({
  field: Object,
});
</script>

<template>
  <div class="col-12">
    <h3 class="border-bottom">{{ props.field.field_elements.title }}</h3>
  </div>
</template>
