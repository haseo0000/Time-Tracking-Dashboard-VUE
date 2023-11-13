<template>
  <div class="timetracker__container">
    <ProfileCard :timeSelected="timeSelected" :handleSelectedTime="handleSelectedTime" />
    <template v-for="data in datas" :key="data.title">
      <TimeDetailsCard :data="data" :timeSelected="timeSelected" />
    </template>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

import ProfileCard from "../components/ProfileCard.vue";
import TimeDetailsCard from "../components/TimeDetailsCard.vue";

import TimeTrackerData from "../data.json";

interface Time {
  current: number;
  previous: number;
}

export interface TimeTrackerDataT {
  title: string;
  timeframes: {
    daily: Time;
    weekly: Time;
    monthly: Time;
  };
}

const datas: TimeTrackerDataT[] = TimeTrackerData;
const timeSelected = ref("Weekly");

const handleSelectedTime = (time: string) => {
  timeSelected.value = time;
};
</script>

<style scoped>
.timetracker__container {
  margin-top: 2rem;
  display: grid;
  gap: 20px;
}

@media (min-width: 1024px) {
  .timetracker__container {
    grid-template-columns: repeat(4, 1fr);
  }
}
</style>
