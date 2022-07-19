<template>
  <li class="transition ease-in duration-300 relative">
    <span
      class="finish-position flex items-center text-6xl absolute left-0 top-0 bottom-0"
      v-if="member.finishPosition > 0 && member.isFinish"
    >
      {{ member.finishPosition }}
    </span>
    <span
      class="cockroach inline-flex flex-col absolute left-0 w-10 h-10"
      :style="{left: member.leftPosition + 'px', marginTop: member.topPosition + 'px'}"
    >
      <span
        class="name px-1 py-1 leading-3 text-white text-xs"
        :style="{background: bgColor}"
      >{{ member.name }}</span>
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
        <path
          d="M511.988 288.9c-.478 17.43-15.217 31.1-32.653 31.1H424v16c0 21.864-4.882 42.584-13.6 61.145l60.228 60.228c12.496 12.497 12.496 32.758 0 45.255-12.498 12.497-32.759 12.496-45.256 0l-54.736-54.736C345.886 467.965 314.351 480 280 480V236c0-6.627-5.373-12-12-12h-24c-6.627 0-12 5.373-12 12v244c-34.351 0-65.886-12.035-90.636-32.108l-54.736 54.736c-12.498 12.497-32.759 12.496-45.256 0-12.496-12.497-12.496-32.758 0-45.255l60.228-60.228C92.882 378.584 88 357.864 88 336v-16H32.666C15.23 320 .491 306.33.013 288.9-.484 270.816 14.028 256 32 256h56v-58.745l-46.628-46.628c-12.496-12.497-12.496-32.758 0-45.255 12.498-12.497 32.758-12.497 45.256 0L141.255 160h229.489l54.627-54.627c12.498-12.497 32.758-12.497 45.256 0 12.496 12.497 12.496 32.758 0 45.255L424 197.255V256h56c17.972 0 32.484 14.816 31.988 32.9zM257 0c-61.856 0-112 50.144-112 112h224C369 50.144 318.856 0 257 0z"
        />
      </svg>
    </span>
  </li>

</template>

<script setup>
import { defineProps, computed} from 'vue'

  const props = defineProps({
    member: Object,
  });

  const bgColor = computed(() => {
    return '#' + Math.floor(Math.random()*16777215).toString(16)
  })

</script>

<style scoped lang="scss">

li {
  border: 3px solid #034c81;
  border-width: 3px 0 3px 0;
  height: 90px;
}

span.cockroach {
  top: 50%;
  transform: translateY(-30%);
  transition: all 0.2s ease;

  span.name {
    position: absolute;
    left: 50%;
    top: -50%;
    white-space: nowrap;
    transform: translateX(-50%);
    border-radius: 5px;
  }

  svg {
    max-width: 100%;
    max-height: 100%;
    transform: rotate(90deg);
  }
}



</style>
