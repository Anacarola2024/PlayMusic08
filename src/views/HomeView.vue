
<template>
  <div class="home">
    <AudioPlayer />
  </div>
</template>

<script>
import AudioPlayer from "@/components/AudioPlayer.vue";

export default {
  name: "Home",
  components: {
    AudioPlayer,
  },
};
</script>

<style scoped>
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
