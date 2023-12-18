<script lang="ts" setup>
import { Gender, Popularity, Length, names, Category } from "~/data";

interface OptionsState {
  gendar: Gender;
  popularity: Popularity;
  length: Length;
}

const options = reactive<OptionsState>({
  gendar: Gender.GIRL,
  popularity: Popularity.UNIQUE,
  length: Length.SHORT,
});

const computeSelectedNames = (): void => {
  const filteredNames = names
    .filter((name) => name.gender === options.gendar)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      return name.length === options.length;
    });

  selectedNames.value = filteredNames.map((n) => n.name);
};

const selectedNames = ref<string[]>([]);

interface OptionsArray {
  title: string;
  category: Category;
  buttons: Gender[] | Popularity[] | Length[];
}

const optionsArray: OptionsArray[] = [
  {
    title: "1) Choose a gendar",
    category: Category.GENDER,
    buttons: [Gender.GIRL, Gender.UNISEX, Gender.BOY],
  },
  {
    title: "2) Choose the name's popularity",
    category: Category.POPULARITY,
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3) Choose name's length",
    category: Category.LENGTH,
    buttons: [Length.LONG, Length.SHORT, Length.ALL],
  },
];

const removeName = (idx: number): void => {
  selectedNames.value.splice(idx, 1);
};
</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" button bellow</p>
    <div class="options-container">
      <baby-option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :options="options"
      />

      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>

    <div class="cards-container">
      <card-name
        v-for="(name, idx) in selectedNames"
        :key="name"
        :name="name"
        @remove="removeName(idx)"
      />
    </div>
  </div>
</template>

<style scoped lang="scss">
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
  h1 {
    font-size: 3rem;
  }
  .options-container {
    background-color: rgb(255, 238, 236);
    border-radius: 2rem;
    padding: 1rem;
    width: 95%;
    margin: 0 auto;
    margin-top: 4rem;
    position: relative;
    .primary {
      background-color: rgb(249, 87, 89);
      color: white;
      border-radius: 6.5rem;
      border: none;
      padding: 0.75rem 4rem;
      font-size: 1rem;
      margin-top: 1rem;
      cursor: pointer;
    }
  }
  .cards-container {
    display: flex;
    margin-top: 3rem;
    flex-wrap: wrap;
  }
}
</style>
