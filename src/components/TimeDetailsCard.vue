<template>
  <div class="timedetails_card__container" :data-bg-type="title">
    <img :src="getTitleIcon" alt="icon-work" width="50" />
    <div class="timedetail__container">
      <div>
        <span>{{ title }}</span>
        <img src="@/assets/images/icon-ellipsis.svg" alt="icon-ellipsis" height="5" />
      </div>
      <div>
        <span class="currentTime">{{ getCurrentTime }}hrs</span>
        <span>Last {{ getNameTime }} - {{ getPreviousTime }}hrs</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { TimeTrackerDataT } from "@/views/TimeTrackerView.vue";
import { computed } from "vue";

const props = defineProps<{
  data: TimeTrackerDataT;
  timeSelected: string;
}>();

const title = props.data.title;

const getTitleIcon = computed(() => {
  const base = "images/";

  switch (title) {
    case "Work":
      return base + "icon-work.svg";
    case "Play":
      return base + `icon-play.svg`;
    case "Study":
      return base + `icon-study.svg`;
    case "Exercise":
      return base + `icon-exercise.svg`;
    case "Social":
      return base + `icon-social.svg`;
    case "Self Care":
      return base + `icon-self-care.svg`;
  }
});

const getCurrentTime = computed(() => {
  switch (props.timeSelected) {
    case "Daily":
      return props.data.timeframes.daily.current;
    case "Weekly":
      return props.data.timeframes.weekly.current;
    case "Monthly":
      return props.data.timeframes.monthly.current;
  }
});

const getPreviousTime = computed(() => {
  switch (props.timeSelected) {
    case "Daily":
      return props.data.timeframes.daily.previous;
    case "Weekly":
      return props.data.timeframes.weekly.previous;
    case "Monthly":
      return props.data.timeframes.monthly.previous;
  }
});

const getNameTime = computed(() => {
  switch (props.timeSelected) {
    case "Daily":
      return "Day";
    case "Weekly":
      return "Week";
    case "Monthly":
      return "Month";
  }
});
</script>

<style scoped>
.timedetails_card__container {
  padding-top: 1.5rem;
  border-radius: 10px;
  position: relative;
  overflow: hidden;
}

.timedetails_card__container > img {
  position: absolute;
  top: -10px;
  right: 20px;
}

.timedetail__container {
  background: #1d204b;
  border-radius: inherit;
  padding: 1rem;
  position: relative;
}

.timedetail__container > div {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.timedetail__container > div > img {
  cursor: pointer;
}

.currentTime {
  font-size: 1.5em;
  color: #fff;
}

.timedetails_card__container[data-bg-type="Work"] {
  background: hsl(15, 100%, 70%);
}
.timedetails_card__container[data-bg-type="Play"] {
  background: hsl(195, 74%, 62%);
}
.timedetails_card__container[data-bg-type="Study"] {
  background: hsl(348, 100%, 68%);
}
.timedetails_card__container[data-bg-type="Exercise"] {
  background: hsl(145, 58%, 55%);
}
.timedetails_card__container[data-bg-type="Social"] {
  background: hsl(264, 64%, 52%);
}
.timedetails_card__container[data-bg-type="Self Care"] {
  background: hsl(43, 84%, 65%);
}

@media (min-width: 1024px) {
  .timedetail__container {
    height: 100%;
  }

  .timedetail__container > *:not(:first-child) {
    flex-direction: column;
    align-items: flex-start;
  }

  .currentTime {
    font-size: 2em;
  }
}
</style>
