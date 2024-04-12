<script>
import { reactive, toRefs } from "vue";
import systemData from "@/json/atkritumu-atlaujas-iesniegums-pub.json";
import TextField from "@/elements/TextField.vue";
import SubtitleField from "@/elements/SubtitleField.vue";
import SelectField from "@/elements/SelectField.vue";
import DatalistGroup from "@/elements/DatalistGroup.vue";
import DateField from "@/elements/DateField.vue";
import CheckboxField from "@/elements/CheckboxField.vue";
import TextareaField from "@/elements/TextareaField.vue";

export default {
  name: "SystemForm",
  components: {
    TextField,
    SubtitleField,
    SelectField,
    DatalistGroup,
    DateField,
    CheckboxField,
    TextareaField,
    // Register other components
  },
  setup() {
    // Ensure systemData structure matches expectations
    const safeSystemData = systemData || { tools: [], form: [], accordion: [] };
    const system = reactive(safeSystemData);

    // Initialize each accordion item's 'show' property
    if (system.accordion && system.accordion.length > 0) {
      system.accordion.forEach((item) => (item.show = false));
    }

    const submitForm = () => {
      // Handle form submission logic here
    };

    const toggleAccordion = (section) => {
      const item = system.accordion.find((i) => i.section === section);
      if (item) {
        item.show = !item.show;
      }
    };

    return {
      ...toRefs(system),
      submitForm,
      toggleAccordion,
    };
  },
};
</script>

<template>
  <div class="container system-form text-start">
    <h1 class="my-4" v-html="title"></h1>

    <div class="form-tools mb-3 row">
      <div
        v-for="(tool, index) in tools"
        :class="tool.col"
        :key="`tool-${index}`"
      >
        <button
          v-if="tool.type === 'button'"
          :class="tool.field_elements.class"
        >
          <i :class="tool.field_elements.icon"></i>
          {{ tool.field_elements.name }}
        </button>
        <!-- Implement dropdown here if needed -->
      </div>
    </div>

    <div class="card mt-3 mb-3 bg-body-tertiary">
      <div class="card-body pt-1">
        <form @submit.prevent="submitForm">
          <div class="row">
            <div
              v-for="(field, index) in form"
              :class="field.col"
              :key="`field-${index}`"
              class="mb-3"
            >
              <SubtitleField v-if="field.type === 'subtitle'" :field="field" />

              <TextField v-else-if="field.type === 'text'" :field="field" />

              <SelectField v-else-if="field.type === 'select'" :field="field" />

              <DatalistGroup
                v-else-if="field.type === 'datalist-group'"
                :field="field"
              />

              <DateField v-else-if="field.type === 'date'" :field="field" />

              <CheckboxField
                v-else-if="field.type === 'checkbox'"
                :field="field"
              />

              <TextareaField
                v-else-if="field.type === 'textarea'"
                :field="field"
              />
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
