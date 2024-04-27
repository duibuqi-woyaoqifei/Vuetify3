<template>
  <div class="box">
    <p class="mb-5 text-h7">Now playing</p>
    <v-avatar :class="avatarSpinClassName" size="200" variant="flat">
      <v-img :src="props.item.cover" alt="John" cover></v-img>
    </v-avatar>
    <p class="text-h6 mt-5">{{ props.item.title }}</p>
    <p class="text-grey-lighten-2 font-weight-thin mb-10">{{ props.item.artist }}</p>
    <v-btn :ripple="false" variant="plain" @click="ChangeStatus()"><v-icon size="40" :icon="isPlayingIcon"></v-icon></v-btn>
    <audio :src="props.item.file" preload="auto" loop></audio>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const props = defineProps<{
  item: {
    id: string;
    title: string;
    artist: string;
    file: string;
    cover?: string;
    isFavourite?: number;
  };
}>();

const isPlayingIcon = ref("mdi-play");
const avatarSpinClassName = ref("");
const ChangeStatus = (order?: string) => {
  const audioBtn = document.querySelector("audio");
  if (order === "pause") {
    isPlayingIcon.value = "mdi-play";
    avatarSpinClassName.value = "";
    audioBtn?.pause();
    return;
  }
  isPlayingIcon.value = isPlayingIcon.value === "mdi-play" ? "mdi-pause" : "mdi-play";
  avatarSpinClassName.value = avatarSpinClassName.value === "spin" ? "" : "spin";

  if (isPlayingIcon.value === "mdi-pause") {
    audioBtn?.play();
  } else {
    audioBtn?.pause();
  }
};

defineExpose({ ChangeStatus });
</script>

<style lang="sass" scoped>
.box
  width: 100%
  height: 100%
  display: flex
  justify-content: center
  flex-direction: column
  align-items: center

.spin
  animation: spin 12s linear infinite

@keyframes spin
  from
    transform: rotate(0deg)
  to
    transform: rotate(360deg)
</style>
