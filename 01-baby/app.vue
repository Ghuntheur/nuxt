<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Chosse your options and click "Find names" button below</p>

    <div class="options-container">
      <Option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :options="options"
      />

      <button class="primary" @click="computeSelectedNames">Find names</button>
    </div>

    <div class="cards-container">
      <CardName
        v-for="name in selectedNames"
        :key="name"
        :name="name"
        class="card"
        @remove="removeName"
      >
      </CardName>
    </div>
    <pre></pre>
  </div>
</template>

<script setup lang="ts">
import { Gender, Popularity, Length, names } from '@/data'

interface OptionsState {
  gender: Gender
  popularity: Popularity
  length: Length
}

const options = reactive<OptionsState>({
  gender: Gender.BOY,
  popularity: Popularity.UNIQUE,
  length: Length.LONG
})

const selectedNames = ref<string[]>([])

const optionsArray = [
  {
    title: '1) Choose a gender',
    category: 'gender',
    buttons: Object.values(Gender)
  },
  {
    title: "2) Choose the name's popularity",
    category: 'popularity',
    buttons: Object.values(Popularity)
  },
  {
    title: "3) Choose the name's length",
    category: 'length',
    buttons: Object.values(Length)
  }
]

const computeSelectedNames = () => {
  selectedNames.value = names
    .filter(
      (item) =>
        item.gender === options.gender && item.popularity === options.popularity
    )
    .filter((item) =>
      options.length === Length.ALL ? true : item.length === options.length
    )
    .map((value) => value.name)
}

const removeName = (name) => {
  selectedNames.value = selectedNames.value.filter((item) => item !== name)
}
</script>

<style scoped>
.container {
  font-family: Arial, Arial, Helvetica, sans-serif;
  color: rgba(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 3rem;
}

.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 99%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}

.option-container {
  margin-bottom: 2rem;
}

.primary {
  background: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.7rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.cards-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}
</style>
