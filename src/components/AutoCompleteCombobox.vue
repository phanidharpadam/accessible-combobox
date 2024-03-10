<template>
  <h1>combobox example</h1>
  <label for="cb-input">State</label>
  <div class="combobox combobox-list">
    <div class="cb-group">
      <input
        id="cb-input"
        type="text"
        v-model="inputText"
        role="combobox"
        aria-autocomplete="list"
        aria-expanded="false"
        aria-controls="cb-listbox"
        @focus="handleInputFocus"
        @blur="handleInputBlur"
      />
      <button
        id="cb-button"
        tabindex="-1"
        aria-label="States"
        :aria-expanded="showListBox"
        aria-controls="cb-listbox"
        @click="toggleListBox"
      >
        <span class="fa fa-caret-down" aria-hidden="true"></span>
      </button>
    </div>
    <ul
      v-show="showListBox"
      ref="listBoxElement"
      id="cb-listbox"
      role="listbox"
      aria-label="States"
    >
      <li
        v-for="listItem in filteredListItems"
        :key="listItem.value"
        :id="`lb-${listItem.value}`"
        role="option"
      >
        {{ listItem.text }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, toRefs, computed } from "vue";

const props = defineProps({
  id: {
    type: String,
    required: false,
  },
  name: {
    type: String,
    required: false,
  },
  items: {
    type: Array,
    required: false,
  },
});

const { id, name, items } = toRefs(props);

const listBoxElement = ref("");
const inputText = ref("");
const showListBox = ref(false);

const filteredListItems = computed(() => {
  return inputText.value === ""
    ? items.value
    : items.value.filter((item) =>
        item.text.toLowerCase().includes(inputText.value.toLowerCase())
      );
});

const toggleListBox = () => {
  showListBox.value = !showListBox.value;
};

const handleInputFocus = () => {
  showListBox.value = true;
};

const handleInputBlur = () => {
  showListBox.value = false;
};
</script>

<style lang="scss">
$width: 14rem;

.combobox-list {
  position: relative;
}
.combobox {
  input,
  button {
    outline: none;
    padding: 5px 3px;
    border-color: black;
  }
  input {
    width: $width;
    border-right: none;
  }
  button {
    border-left: none;
    background-color: white;
  }
  button[aria-expanded="true"] {
    span {
      transform: rotate(180deg) translate(0, -3px); /* Your existing transformation */
    }
  }
}

ul[role="listbox"] {
  margin: 0;
  padding: 0;
  position: absolute;
  top: 100%;
  list-style: none;
  background-color: white;
  box-sizing: border-box;
  border: 2px currentcolor solid;
  border-top: none;
  max-height: 250px;
  width: $width + 1.52rem;
  overflow: scroll;
  overflow-x: hidden;
  font-size: 87.5%;
  cursor: pointer;

  li[role="option"] {
    margin: 0;
    padding-left: 3px;
    padding-top: 2px;
    padding-bottom: 2px;
  }

  li:hover {
    background-color: blue;
    color: white;
  }
}
</style>
