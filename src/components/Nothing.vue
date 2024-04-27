<template>
  <div class="dev">
    <div class="develop">
      <v-icon class="text-h1" icon="mdi-alert-circle-outline"></v-icon>
      <p class="text-grey-lighten-1 font-weight-bold mt-3">NOTHING...</p>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
</script>

<style lang="sass" scoped>
.dev
  display: flex
  align-items: center
  justify-content: center
  width: 100%
  height: 400px

.develop
  text-align: center
</style>
