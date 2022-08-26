<template>
  <div class="card">
    <h4>{{ name }}</h4>
    <p @click="emit('remove', name)">x</p>
  </div>
</template>

<script lang="ts" setup>
interface Props {
  name: string
}

defineProps<Props>()

const emit = defineEmits(['remove'])
</script>

<style>
.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0.1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}

.card p {
  position: absolute;
  top: -20%;
  left: 92.5%;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.8);
}
</style>
