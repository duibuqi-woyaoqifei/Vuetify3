<template>
  <v-card-text :class="SBoxClass">
    <v-text-field
      v-model="searchContent"
      rounded
      :loading="loading"
      append-inner-icon="mdi-magnify"
      bg-color="grey-darken-3"
      density="compact"
      label="Search"
      hide-details
      single-line
      variant="solo"
      @click:append-inner="onClick"
      @update:focused="onFocus"
      @keyup.enter="onClick"
    ></v-text-field>
  </v-card-text>

  <Nothing v-if="searchResult === 'nothing'"></Nothing>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import Nothing from "@/components/Nothing.vue";
import requests from "@/plugins/axios";

const searchContent = ref("");
const searchResult = ref("");
const loading = ref(false);
const SBoxClass = ref("SBox mt-4");

const getSearchInfo = (params: any = {}) => {
  return requests({
    url: "/search",
    method: "get",
    params,
  });
};

const onClick = () => {
  loading.value = true;

  getSearchInfo({ content: searchContent.value })
    .then((req: any) => {
      setTimeout(() => {
        loading.value = false;
        if (req === "nothing") {
          searchResult.value = req;
        }
      }, 1000);
    })
    .catch((err) => {
      console.log(err);
    });
};

const onFocus = (isFocus: boolean) => {
  if (isFocus) {
    SBoxClass.value = "SBox wider mt-4";
  } else {
    SBoxClass.value = "SBox narrower mt-4";
  }
};
</script>

<style lang="sass" scoped>
.SBox
  width: 60%
  position: relative
  left: 50%
  transform: translateX(-50%)

.wider
  animation: Wider 0.3s forwards

.narrower
  animation: Narrower 0.3s forwards

@keyframes Wider
  from
    width: 60%

  to
    width: 70%

@keyframes Narrower
  from
    width: 70%

  to
    width: 60%
</style>
