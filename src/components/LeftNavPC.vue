<template>
  <div class="logo mx-10 mt-8">
    <v-img :width="40" aspect-ratio="1" cover src="img\logo.png" inline></v-img>
    <h1 class="logo_font">XXXXXX</h1>
  </div>

  <v-list active-class="light" class="mx-10 mt-10" bg-color="transparent" density="compact" mandatory>
    <div class="mb-10" v-for="(listInfo, i) in lists">
      <v-list-subheader class="mb-4 list_title" color="white">
        <h2>{{ listInfo.title }}</h2>
      </v-list-subheader>
      <v-list-item
        class="left_nav mb-1"
        v-for="(item, i2) in listInfo.list"
        :key="i"
        :value="item"
        variant="plain"
        slim
        @click="SelectNav(item.index)"
        :class="item.index === 0 ? defaultClass : ''"
      >
        <template v-slot:prepend>
          <v-icon :icon="item.icon" :color="item.color"></v-icon>
        </template>
        <v-list-item-title v-text="item.text"></v-list-item-title>
      </v-list-item>
    </div>
  </v-list>

  <a href="https://github.com/duibuqi-woyaoqifei/Vuetify3" class="to_github">
    <span class="mr-1" style="letter-spacing: 1px">Github</span>
    <v-icon icon="mdi-github"></v-icon>
  </a>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const index = defineModel<number>({ default: 0 });

const defaultClass = ref("light");

const lists = [
  {
    title: "EXPLORE",
    index: 0,
    list: [
      { index: 0, text: "Discover", icon: "mdi-music-circle" },
      { index: 1, text: "Search", icon: "mdi-magnify" },
      { index: 2, text: "Your Tunes", icon: "mdi-heart" },
    ],
  },
  {
    title: "SERVICES",
    index: 1,
    list: [
      { index: 3, text: "Get The App", icon: "mdi-download" },
      { index: 4, text: "Premium", icon: "mdi-star", color: "yellow" },
      { index: 5, text: "Settings", icon: "mdi-cog" },
    ],
  },
];

const SelectNav = (i: number) => {
  defaultClass.value = "";
  index.value = i;
};
</script>

<style scoped>
.list_title {
  transform: translateX(-16px);
  font-size: 12px;
  letter-spacing: 1px;
}
.light {
  opacity: 100;
}
.to_github {
  position: absolute;
  width: 100px;
  height: 40px;
  line-height: 40px;
  text-align: center;
  left: 50%;
  transform: translateX(-50%);
  bottom: 10px;
}
.left_nav {
  font-size: 11px;
  color: #fff !important;
}
.logo {
  display: flex;
  align-items: center;
}
.logo_font {
  text-transform: uppercase;
  font-weight: 700;
  font-size: 25px;
  letter-spacing: 2px;
  padding-left: 16px;
}
</style>
