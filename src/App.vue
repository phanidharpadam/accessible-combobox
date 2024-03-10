<script setup>
import AutoCompleteCombobox from "./components/AutoCompleteCombobox.vue";
import { ref } from "vue";

const items = ref([
  {
    text: "apple",
    value: "0",
  },
  {
    text: "ball",
    value: "1",
  },
  {
    text: "cat",
    value: "2",
  },
  {
    text: "dog",
    value: "3",
  },
]);
</script>

<template>
  <AutoCompleteCombobox :items="items"></AutoCompleteCombobox>
</template>
