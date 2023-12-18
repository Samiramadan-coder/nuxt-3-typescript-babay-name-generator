<script setup lang="ts">
import { Gender, Popularity, Length, Category } from "~/data";

interface OptionProps {
  option: {
    title: string;
    category: Category;
    buttons: Gender[] | Popularity[] | Length[];
  };
  options: {
    gendar: Gender;
    popularity: Popularity;
    length: Length;
  };
}

const props = defineProps<OptionProps>();

const highlightCat = (val: Gender | Popularity | Length): void => {
  props.options[props.option.category] = val;
};
</script>

<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <div class="options-buttons">
      <button
        v-for="value in option.buttons"
        :key="value"
        :class="options[option.category] === value && 'active'"
        @click="highlightCat(value)"
      >
        {{ value }}
      </button>
    </div>
  </div>
</template>

<style scoped lang="scss">
.option-container {
  margin-bottom: 2rem;
  button {
    background: white;
    outline: 0.15rem solid rgb(249, 87, 89);
    border: none;
    padding: 0.75rem;
    width: 12rem;
    font-size: 1rem;
    color: rgb(27, 60, 138);
    font-weight: 200;
    cursor: pointer;
    &.active {
      background: rgb(249, 87, 89);
      color: white;
    }
    &:first-of-type {
      border-radius: 1rem 0 0 1rem;
    }
    &:last-of-type {
      border-radius: 0 1rem 1rem 0;
    }
  }
}
</style>
