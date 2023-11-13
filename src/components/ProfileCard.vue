<template>
  <div class="profile_card__container">
    <div class="header__container">
      <img src="/images/image-jeremy.png" alt="img-profile" width="50" />
      <div class="profile__container">
        <span class="profile_title">Report for</span>
        <span class="profile_name">Jeremy Robson</span>
      </div>
    </div>
    <div class="bottom__container">
      <template v-for="time in timeline" :key="time">
        <span
          @click="handleSelectedTime(time)"
          :class="{ 'time-selected': timeSelected === time }"
          >{{ time }}</span
        >
      </template>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  timeSelected: string;
  handleSelectedTime: (time: string) => void;
}>();

const timeline = ["Daily", "Weekly", "Monthly"];
</script>

<style scoped>
.profile_card__container {
  background: #1d204b;
  border-radius: 10px;
}

.header__container {
  display: flex;
  align-items: center;
  gap: 10px;
  background: #5746ea;
  border-radius: inherit;
  padding: 1.3rem 1rem;
}

.profile__container {
  display: grid;
}
.profile_title {
  font-size: 0.6em;
}

.profile_name {
  color: #fff;
}

.bottom__container {
  display: flex;
  justify-content: space-between;
  padding: 1rem;
}

.bottom__container > * {
  cursor: pointer;
}

.time-selected {
  color: #fff;
}

@media (min-width: 1024px) {
  .profile_card__container {
    grid-row: 1 / 3;
  }

  .header__container {
    flex-direction: column;
    align-items: flex-start;
    padding-bottom: 3rem;
  }

  .profile_name {
    font-size: 1.75em;
    line-height: 1em;
  }

  .bottom__container {
    flex-direction: column;
    gap: 10px;
  }
}
</style>
