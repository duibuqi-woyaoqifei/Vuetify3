<template>
  <v-container class="bg-surface-variant" fluid>
    <v-row style="height: 100vh; background-color: #db1d40" no-gutters align="center" justify="center">
      <v-col cols="3" class="left_box">
        <LeftNavPC v-model="currentNav" v-if="windowWidth > 1200"></LeftNavPC>
      </v-col>

      <v-col class="middle_box">
        <Discover ref="discoverRef" :items="items" v-if="currentNav === 0" @select="PlayMusic"></Discover>
        <Search v-else-if="currentNav === 1"></Search>
        <YourTunes v-else-if="currentNav === 2"></YourTunes>
        <Developing v-else></Developing>
      </v-col>

      <v-col cols="3" class="right_box">
        <div class="black">
          <v-col cols="3" class="right_box_">
            <Player ref="playerRef" v-if="pendingItem" :item="pendingItem"></Player>
          </v-col>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts" setup>
import { ref, watch } from "vue";
import Discover from "@/components/Discover.vue";
import Search from "@/components/Search.vue";
import YourTunes from "@/components/YourTunes.vue";
import Developing from "@/components/Developing.vue";
import LeftNavPC from "@/components/LeftNavPC.vue";
import Player from "@/components/Player.vue";

// 监听窗口宽度
const windowWidth = ref(window.innerWidth);
window.onresize = function (e) {
  windowWidth.value = window.innerWidth;
};

// 左侧导航索引
const currentNav = ref(0);

// 音乐列表数据
const items = ref([
  {
    id: "JJ10000",
    cover: "/music/Pop/JJ10000/cover.jpg",
    file: "/music/Pop/JJ10000/HVOB - Dogs.flac",
    title: "Dogs",
    artist: `HVOB`,
  },
]);
const pendingItem = ref({
  id: "JJ10000",
  cover: "/music/Pop/JJ10000/cover.jpg",
  file: "/music/Pop/JJ10000/HVOB - Dogs.flac",
  title: "Dogs",
  artist: `HVOB`,
});
const discoverRef = ref();
const playerRef = ref();
function PlayMusic(item: any) {
  if (pendingItem.value.id === item.id) return console.log(1);
  playerRef.value.ChangeStatus("pause");
  pendingItem.value = item;
}
</script>

<style scoped>
.bg-surface-variant {
  position: relative;
  padding: 0;
}

.left_box {
  background-color: #7e2236;
  height: 744px;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
  max-width: 300px;
  margin-left: 50px;
  position: relative;
}

.middle_box {
  background-color: #232323;
  height: 744px;
  max-width: 800px;
  min-width: 300px;
  overflow-y: scroll;
}
.middle_box::-webkit-scrollbar-button {
  display: none !important; /* 隐藏上下方向标志 */
}

.middle_box::-webkit-scrollbar-track {
  background: transparent; /* 透明背景 */
}

.right_box {
  background-color: #db1d40;
  height: 744px;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  max-width: 300px;
  margin-right: 50px;
  min-width: 200px;
}

.right_box_ {
  background-color: #db1d40;
  height: 744px;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  max-width: 300px;
  min-width: 200px;
}

.red {
  background-color: #fff;
  height: 100vh;
  width: 100%;
}

.black {
  background-color: #232323;
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  display: flex;
  align-items: center;
}

@media only screen and (max-width: 1200px) {
  .left_box {
    flex-basis: 60px;
    margin-left: 30px;
    height: 865px;
  }

  .middle_box {
    height: 865px;
  }

  .right_box {
    flex-basis: 280px;
    margin-right: 30px;
    height: 865px;
  }

  .right_box_ {
    flex-basis: 280px;
    height: 865px;
  }
}
</style>
