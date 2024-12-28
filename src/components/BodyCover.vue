<script setup lang="ts">
import { ref } from "vue";
defineProps({
  tracksList: Object,
});

const isBurgerMenuOpen = ref(false); // State for burger menu visibility
// Toggle burger menu visibility
function toggleBurgerMenu() {
  isBurgerMenuOpen.value = !isBurgerMenuOpen.value;
}

const tracks = ref([]);

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

// console.log(tracks);
</script>

<template>
  <div class="body__cover">
    <!-- Burger Button -->
    <button class="burger-button" @click="toggleBurgerMenu">
      <i class="fa" :class="[isBurgerMenuOpen ? 'fa-times' : 'fa-bars']"></i>
    </button>

    <!-- Album Cover -->
    <img src="./images/maxresdefault.jpg" alt="Album cover" class="album-cover" />

    <div class="range"></div>
    <!-- Magnifying Glass -->
    <a class="magnifying-glass" href="#"><i class="fa fa-search"></i></a>
  </div>

  <!-- Album Tracks List -->
  <div v-show="isBurgerMenuOpen" class="album">
    <div class="burger-menu" :class="{ 'burger-menu--open': isBurgerMenuOpen }">
      <ul>
        <li v-for="track in tracks" :key="track.id" class="track">
          {{ track.track_number }}. {{ track.name }} -
          {{ track.artists[0]?.name || "Unknown Artist" }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@function remy($value, $base: 16px) {
  @return ($value / $base) * 1rem;
}

// Mixins
@mixin transition($prop: all, $duration: 0.25s, $timing: cubic-bezier(0.4, 0, 1, 1)) {
  transition: $prop $duration $timing;
}

$radius: remy(4px);
$color-red: #d30320;

.track {
  color: black;
  font-size: 0.9rem;
}

.body__cover {
  position: relative;
  img {
    display: block;
    max-width: 100%;
    height: auto;
  }

  .burger-button {
    position: absolute;
    top: 10px; /* Adjust as needed */
    left: 10px; /* Adjust as needed */
    border: none;
    font-size: 1.7rem;
    padding: 7px 10px;
    border-radius: 4px;
    color: white;
    background-color: transparent;
    cursor: pointer;
  }

  .burger-menu {
    position: fixed; /* Меню фиксировано на экране */
    top: 0;
    left: -300px; /* Изначально спрятано за левым краем экрана */
    width: 300px;
    height: 100%;
    background: rgba(0, 0, 0, 0.9);
    color: white;
    overflow-y: auto;
    transition: left 0.3s ease; /* Анимация при открытии */
    z-index: 1000;
    padding: 20px;
  }

  .burger-menu--open {
    left: 0; /* Когда меню открыто, оно появляется слева от экрана */
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;

    li {
      margin-bottom: 15px;
      font-size: 1rem;
    }
  }

  .magnifying-glass {
    position: absolute;
    top: 10px;
    right: 10px;
    color: white;
    font-size: 1.4rem;
    padding: 0px 10px;
    border-radius: 4px;
    text-decoration: none;
  }
}

.album-cover {
  width: 320px;
  height: 320px;
}

.range {
  position: relative;
  top: -1.5rem;
  right: 0;
  left: 0;
  margin: auto;
  background: rgba(#fff, 0.95);
  width: 80%;
  height: remy(2px);
  border-radius: $radius;
  cursor: pointer;

  &:before,
  &:after {
    content: "";
    position: absolute;
    cursor: pointer;
  }

  &:before {
    width: 3rem;
    height: 100%;
    background: linear-gradient(to right, rgba($color-red, 0.5), rgba($color-red, 0.85));
    border-radius: $radius;
    overflow: hidden;
  }

  &:after {
    top: remy(-6px);
    left: 3rem;
    z-index: 3;
    width: remy(14px);
    height: remy(14px);
    background: #fff;
    border-radius: 50%;
    box-shadow: 0 0 3px rgba(0, 0, 0, 0.15), 0 2px 4px rgba(0, 0, 0, 0.15);

    @include transition;
  }

  &:focus,
  &:hover {
    &:after {
      background: rgba($color-red, 0.95);
    }
  }
}
</style>
