<template>
  <div class="filter">
    <!-- début du dropdown -->
    <div class="filter-select">
      <select class="filter-select-input" v-model="section">
        <option
          v-for="(section, index) in sections"
          :key="index"
          :value="section"
        >
          {{ capitalize(section) }}
        </option>
      </select>
    </div>
    <!-- fin du dropdown -->
    <div>
      <button class="filter-button" @click="fetch" >Retrieve</button>
    </div>
  </div>
</template>

<script>
import { computed } from "vue";
import sectionsData from "./section";

export default {
  props: {
    modelValue: String,
    fetch: Function,
  },
  setup(props, { emit }) {
    const section = computed({
      get: () => props.modelValue,
      set: (value) => emit("update:modelValue", value),
    });

    return {
      section,
    };
  },
  data() {
    return {
      sections: sectionsData,
    };
  },
  methods: {
    capitalize(value) {
      if (!value) return "";
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/variable";

.filter {
  display: flex;
  justify-content: center;
  &-select {
    position: relative;
    display: flex;
    align-items: center;
    &-input {
      border: none;
      border-radius: 5px;
      font-size: 20px;
      padding: 10px 40px 10px 10px;
      margin: 10px;
      appearance: none;
      &:hover {
        cursor: pointer;
      }
    }
    &::after {
      content: '';
      background-image: url("../assets/images/arrow-down.svg");
      background-size: cover;
      width: 20px;
      height: 20px;
      position: absolute;
      right: 20px;
    }
  }
  &-button {
    border: none;
    margin: 10px;
    padding: 10px 30px;
    font-size: 20px;
    background-color: $color5;
    border-radius: 5px;
    &:hover {
      background-color: $color4;
      cursor: pointer;
    }
  }
}
</style>
