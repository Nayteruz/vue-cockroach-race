<template>
  <div class="fixed z-50 left-0 right-0 top-0 bottom-0 flex flex-col items-center justify-center bg-gray-500/30" v-if="userSelectFighter === null">
    <div class="inner-block inline-flex flex-col items-center w-4/6 p-6 bg-sky-900 rounded-2xl">
      <h2 class="text-5xl mb-5">Choose your fighter</h2>
      <ul class="flex flex-row gap-3">
        <li v-for="fighter in fighters" :key="fighter.name">
          <span class="block p-3 cursor-pointer bg-green-500 rounded-2xl hover:bg-green-800" @click="select(fighter)">{{ fighter.name }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import {defineProps, defineEmits, ref} from "vue";

  const props = defineProps(['fighters']);
  const emit = defineEmits(['selectFighter']);

  const userSelectFighter = ref(null);

  const select = (f) => {
    userSelectFighter.value = f;
    emit('selectFighter', userSelectFighter.value)
  }

</script>

<style scoped>

</style>