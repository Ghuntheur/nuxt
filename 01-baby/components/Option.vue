<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <div class="option-button">
      <button
        v-for="value in option.buttons"
        :key="value"
        :class="{ active: options[option.category] === value }"
        class="option"
        @click="options[option.category] = value"
      >
        {{ value }}
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Gender, Length, Popularity } from '@/data'

interface OptionsProps {
  option: {
    title: string
    category: string
    buttons: Gender[] | Popularity[] | Length[]
  }
  options: {
    gender: Gender
    popularity: Popularity
    length: Length
  }
}

const props = defineProps<OptionsProps>()
</script>

<style>
.option {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}

.option:first-of-type {
  border-top-left-radius: 1rem;
  border-bottom-left-radius: 1rem;
}

.option:last-of-type {
  border-top-right-radius: 1rem;
  border-bottom-right-radius: 1rem;
}

.option.active {
  background: rgb(249, 87, 89);
  color: white;
}
</style>
