<script>
import Pastebin from "./components/Pastebin.vue";
export default {
  components: {
    Pastebin,
  },
};
</script>

<template>
  <div class="vertical">
    <div class="horizontal">
      <Pastebin @click="onclick"></Pastebin>
    </div>
  </div>
</template>

<style scoped>
</style>
