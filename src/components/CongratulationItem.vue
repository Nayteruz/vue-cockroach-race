<template>
  <div class="fixed z-50 left-0 right-0 top-0 bottom-0 flex flex-col items-center justify-center bg-gray-500/30" v-if="show">
    <div class="inner-block inline-flex flex-col items-center w-4/6 p-6 bg-sky-900 rounded-2xl">
      <div class="close absolute right-3 top-3 text-3xl text-emerald-800 bg-white w-7 h-7 flex items-center justify-center rounded-full cursor-pointer" @click="close">×</div>
      <h2 class="text-5xl m-0 py-4">{{ member.name }} заняли {{ member.finishPosition }} место!</h2>
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref, watch} from "vue";

  const props = defineProps(['member', 'isShow']);

  const show = ref(false);

  const close = () => {
    show.value = false;
  }
  watch(() => props.isShow, (nVal) => {
    show.value = nVal;
  })

</script>

<style scoped>

</style>