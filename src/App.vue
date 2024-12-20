<script setup lang="ts">
import { ref } from "vue";
import PlayerFooter from "./components/PlayerFooter.vue";
import ControlsButtons from "./components/ControlsButtons.vue";
import SongInfo from "./components/SongInfo.vue";
import BodyCover from "./components/BodyCover.vue";
import LoginButton from "./components/LoginButton.vue";

const tracks = ref([]);

const clientId = "3a125a5c879d4e6f9eb662422e6548e8";
const redirectUri = "http://localhost:5173/callback";
const scopes = "user-read-playback-state user-modify-playback-state user-read-currently-playing";

const authUrl = `https://accounts.spotify.com/authorize?client_id=${clientId}&response_type=token&redirect_uri=${encodeURIComponent(
  redirectUri
)}&scope=${encodeURIComponent(scopes)}`;

const accessToken = new URL(window.location.href).hash
  .substring(1)
  .split("&")
  .find((item) => item.startsWith("access_token"))
  ?.split("=")[1];

if (accessToken) localStorage.setItem("spotifyAccessToken", accessToken);
const token = localStorage.getItem("spotifyAccessToken");

async function fetchAlbum(albumId: string) {
  if (!token) return console.error("No access token available");

  const response = await fetch(`https://api.spotify.com/v1/albums/${albumId}`, {
    headers: { Authorization: `Bearer ${token}` },
  });

  if (!response.ok) return console.error("Failed to fetch album", response.status);

  return response.json();
}

async function loadAlbum(albumId: string) {
  const album = await fetchAlbum(albumId);
  console.log(album);
  if (album) tracks.value = album.tracks.items;
}

loadAlbum("4jn3qmJgUFSWyXzJM8bgF9");
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
