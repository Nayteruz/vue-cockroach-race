<template>
  <SelectFighter
    :fighters="members"
    @selectFighter="setUserFighter"
  />
  <CongratulationItem
    :member="userFighter"
    :isShow="isAllFinish()"
  />
  <ul
      class="lider-table p-0 m-0 list-none flex flex-col w-full gap-1 mb-3"
  >
    <LiderItem
        :leader="leader"
        v-for="leader in leaders"
        :key="leader.name"
    />
  </ul>
  <ul
      class="race flex flex-col p-0 m-0 list-none gap-1"
      ref="trace"
  >
    <CockroachItem
        v-for="member in members"
        :member="member"
        :key="member.name"
    />
  </ul>
  <div
      class="flex items-center justify-center gap-2 mt-4 buttons"
  >
    <button
        v-if="isStart != true"
        @click="startRound"
        class="px-5 py-2 rounded-full bg-violet-700 outline-none text-white"
    >
      Старт
    </button>
    <button
        v-else-if="isStart == true"
        @click="repeatRound"
        class="px-5 py-2 rounded-full bg-orange-700 outline-none text-white"
    >
      Повтор
    </button>
  </div>
</template>

<script setup>
import CockroachItem from '@/components/CockroachItem.vue'
import LiderItem from "@/components/LiderItem.vue";
import SelectFighter from "@/components/SelectFighter.vue"
import CongratulationItem from "@/components/CongratulationItem.vue"
import {computed, onMounted, ref} from 'vue';


const trace = ref(null);
const fullWidth = ref(0);
const isStart = ref(null);


const members = ref([
  {name: 'Донателло', position: 0, leftPosition: 0, topPosition:0, finishPosition: 0, isFinish: false, userSelected: false},
  {name: 'Рафаэль', position: 0, leftPosition: 0, topPosition:0, finishPosition: 0, isFinish: false, userSelected: false},
  {name: 'Леонардо', position: 0, leftPosition: 0, topPosition:0, finishPosition: 0, isFinish: false, userSelected: false},
  {name: 'Микеланджело', position: 0, leftPosition: 0, topPosition:0, finishPosition: 0, isFinish: false, userSelected: false}
]);

const leaders = computed(() => {
  return [...members.value].sort((a, b) => {
    if(a.finishPosition === 0 && b.finishPosition === 0){
      return b.leftPosition - a.leftPosition
    } else {
      return a.finishPosition - b.finishPosition
    }
  })
})

const userFighter = computed(() => members.value.filter(m=>m.userSelected)[0])

const isAllFinish = () => {
  return !members.value.find(m => !m.isFinish);
}

const shuffleArr = (arr) => {
  return arr.sort(() => (Math.random() > .5) ? 1 : -1);
}

const randomNumber = (min, max) => {
  return parseInt(Math.random() * (max - min) + min);
}

let runInterval;
const startRun = () => runInterval = setInterval(() => {
  members.value.forEach((m) => {
    if (!m.isFinish) {
      if (m.leftPosition >= trace_length.value - 40) {
        m.isFinish = true;
        m.finishPosition = maxFinishPosition();
      } else {
        m.leftPosition += randomNumber(-5, 10);
        m.topPosition += randomNumber(-10, 10);
        if(m.topPosition > 30 || m.topPosition < -30){
          m.topPosition = 0
        }
      }
    }
  })
  if (isAllFinish()) {
    clearInterval(runInterval);
  }
  leaders.value.forEach((l, i) => {
    setTracePosition(l.name, i+1);
  })
}, 50)

const stopRound = () => clearInterval(runInterval);

const setTracePosition = (name, pos) => {
  for (let m of members.value){
    if(m.name === name){
      m.position = pos;
    }
  }
}

const maxFinishPosition = () => {
  return Math.max(...members.value.map(o => o.finishPosition)) + 1;
}

const trace_length = computed(() => {
  return fullWidth.value;
});

const initRound = () => {
  isStart.value = null;
  members.value = shuffleArr(members.value);
  fullWidth.value = trace.value.clientWidth
}

const startRound = () => {
  isStart.value = true;
  startRun();
}

const repeatRound = () => {
  stopRound();
  isStart.value = false;
  for (let member of members.value) {
    member.leftPosition = 0;
    member.position = 0;
    member.finishPosition = 0;
    member.isFinish = false;
  }
}

const setUserFighter = (f) => {
  for (let m of members.value){
    if (m === f) {
      m.name = 'Вы, ' + m.name;
      m.userSelected = true;
    }
  }
}

onMounted(() => {
  initRound();
})

</script>
