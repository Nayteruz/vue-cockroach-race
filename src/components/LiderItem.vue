<template>
  <li
      class="flex items-center gap-1 bg-violet-700 rounded-full w-3/6 "
  >
    <span class="w-10 h-10  flex items-center justify-center text-2xl" >{{ mb }}</span>
    <span class="text-2xl">{{ leader.name }}</span>
  </li>
</template>

<script setup>
import {computed, defineProps} from "vue";
  const props = defineProps({
    leader: Object
  })

  const mb = computed(() => {
    return props.leader.finishPosition ? props.leader.finishPosition : props.leader.position
  })
</script>
