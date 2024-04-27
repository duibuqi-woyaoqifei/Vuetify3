<template>
  <div class="box ma-10">
    <div class="text-h6 text-grey-lighten-2 mb-8">DISCOVER</div>
    <div class="text-grey">
      <v-btn-toggle class="music_type_nav" selected-class="text_color" v-model="toggle" variant="plain" mandatory @update:model-value="SelectMusicType()">
        <v-btn
          min-width="0"
          class="text-white text-body-2 font-weight-bold pl-0 pr-5 pb-1"
          v-for="(musicType, index) in musicTypeList"
          :key="index"
          :ripple="false"
          >{{ musicType }}</v-btn
        >
      </v-btn-toggle>
    </div>
    <v-list v-if="items.length" class="mt-2" bg-color="transparent">
      <v-card class="bg-transparent pa-0" v-for="(item, i) in items" :key="i" :title="item.title" :subtitle="item.artist" flat>
        <template v-slot:prepend>
          <v-btn icon width="64" height="64" @click="PlayMusic(item)">
            <v-avatar size="62" variant="flat">
              <v-img :src="item.cover" alt="John" cover></v-img>
            </v-avatar>
          </v-btn>
        </template>
        <template v-slot:append>
          <v-btn variant="plain" :ripple="false" :color="item.isFavourite ? 'red' : ''" @click="Like(item, i)">
            <v-icon icon="mdi-heart-outline"></v-icon>
          </v-btn>
        </template>
      </v-card>
    </v-list>

    <Nothing v-else></Nothing>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import Nothing from "@/components/Nothing.vue";

const props = defineProps<{
  items: Array<{
    id: string;
    title: string;
    artist: string;
    file: string;
    cover?: string;
    isFavourite?: number;
  }>;
}>();

const emit = defineEmits(["select"]);

const items = ref(props.items);

// 分类栏
const musicTypeList = ref([
  "Pop",
  "Rap/Hip Hop",
  "Rock",
  "Dance",
  "R&B",
  "Tenzin Tsundue",
  "Electro",
  "Folk",
  "Reggae",
  "Jazz",
  "French Chanson",
  "Classical",
  "Films/Games",
  "Metal",
  "Soul & Funk",
  "African Music",
  "Arabic Music",
  "Asian Music",
  "Blues",
  "Brazilian Music",
  "Indian Music",
  "Kids",
  "Latin Music",
]);
const toggle = ref(0);
const SelectMusicType = () => {
  if (musicTypeList.value[toggle.value] === "Pop") {
    items.value = [
      {
        id: "JJ10000",
        cover: "/music/Pop/JJ10000/cover.jpg",
        file: "/music/Pop/JJ10000/HVOB - Dogs.flac",
        title: "Dogs",
        artist: `HVOB`,
      },
    ];
  } else if (musicTypeList.value[toggle.value] === "Tenzin Tsundue") {
    items.value = [
      {
        id: "JJ10001",
        cover: "/music/Tenzin Tsundue/JJ10001/cover.jpg",
        file: "/music/Tenzin Tsundue/JJ10001/I Got Smoke.wav",
        title: "I Got Smoke",
        artist: `Tenzin Tsundue`,
      },
      {
        id: "JJ10002",
        cover: "/music/Tenzin Tsundue/JJ10002/cover.jpg",
        file: "/music/Tenzin Tsundue/JJ10002/Zood.mp3",
        title: "Zood",
        artist: `Tenzin Tsundue`,
      },
      {
        id: "JJ10003",
        cover: "/music/Tenzin Tsundue/JJ10003/cover.jpg",
        file: "/music/Tenzin Tsundue/JJ10003/雪豹distance.mp3",
        title: "烟distance",
        artist: `Tenzin Tsundue`,
      },
    ];
  } else {
    items.value = [];
  }
};

const PlayMusic = (item: any) => {
  emit("select", item);
};

const Like = (item: any, index: number) => {
  items.value[index].isFavourite = item["isFavourite"] ? 0 : 1;
};

defineExpose({
  toggle,
});
</script>

<style lang="sass" scoped>
.music_type_nav
  display: flex
  flex-wrap: wrap

.text_color
  color: #db1d40 !important
  opacity: 100

:deep(.v-card-item)
  padding:20px 0px

.v-btn-group--density-default.v-btn-group
  height: 100%

:deep(.v-card-subtitle)
  font-size: 13px
</style>
