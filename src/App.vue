<script setup lang="ts">
import { ref } from "vue";
import PlayerFooter from "./components/PlayerFooter.vue";
import ControlsButtons from "./components/ControlsButtons.vue";
import SongInfo from "./components/SongInfo.vue";
import BodyCover from "./components/BodyCover.vue";
import LoginButton from "./components/LoginButton.vue";


</script>
<template>
  <div class="wrapper">
    <div class="player__container">
      <div class="player__body">
        <!-- Cover Section -->
        <BodyCover :tracksList="tracks"></BodyCover>
        <!-- Song Info -->
        <SongInfo></SongInfo>
        <!-- Controls -->
        <ControlsButtons></ControlsButtons>
      </div>

      <!-- Footer -->
      <PlayerFooter></PlayerFooter>
    </div>
    <LoginButton></LoginButton>
  </div>
</template>

<style scoped lang="scss">
// Functions
@function remy($value, $base: 16px) {
  @return ($value / $base) * 1rem;
}

// Mixins
@mixin transition($prop: all, $duration: 0.25s, $timing: cubic-bezier(0.4, 0, 1, 1)) {
  transition: $prop $duration $timing;
}

// Colors
$color-black: #212121;
$color-blue: #03a9f4;
$color-red: #d30320;
$radius: remy(4px);

// Variables
$boxshadow-0: 0 1px 3px -5px rgba(0, 0, 0, 0.13), 0 1px 3px -10px rgba(0, 0, 0, 0.23);
$boxshadow-1: 0 3px 6px -5px rgba(0, 0, 0, 0.16), 0 3px 6px -10px rgba(0, 0, 0, 0.23);
$boxshadow-2: 0 10px 20px -5px rgba(0, 0, 0, 0.19), 0 6px 6px -10px rgba(0, 0, 0, 0.23);
$boxshadow-3: 0 14px 28px -5px rgba(0, 0, 0, 0.25), 0 10px 10px -10px rgba(0, 0, 0, 0.22);

// Base
html {
  font-size: 16px;
}

body {
  font-family: "Roboto", Arial, Verdana, sans-serif;
  background: $color-red;
}

a {
  text-decoration: none;
}

.wrapper {
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  // width: 100%;
  height: 100vh;
  background-image: url("../../src/components/images/entre-dos-tierras-till-lindemann.jpg");
}

.player__container {
  // margin-top: auto;
  margin-right: auto;
  margin-left: auto;
  max-width: remy(320px);
  background: #fff;
  border-radius: $radius;
  box-shadow: $boxshadow-2;
}
</style>
