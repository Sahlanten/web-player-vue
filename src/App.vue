<script setup lang="ts">
import { ref, onMounted } from "vue";

// Import necessary components from Naive UI
import { MenuOutlined } from "@vicons/antd";
import { NButton, NIcon, NDrawer, NMenu } from "naive-ui";

const isMenuOpen = ref(false); // State for drawer visibility
const selectedMenu = ref(null); // Currently selected menu item

// Menu options (dynamic or static, depending on your app)
const menuOptions = [
  {
    label: "Home",
    key: "home",
    icon: () => h(MenuOutlined),
  },
  {
    label: "About",
    key: "about",
    icon: () => h(MenuOutlined),
  },
  {
    label: "Services",
    key: "services",
    children: [
      { label: "Web Development", key: "web" },
      { label: "Mobile Development", key: "mobile" },
    ],
  },
  {
    label: "Contact",
    key: "contact",
  },
];


</script>

<template>
  <div class="wrapper">
    <div class="player__container">
      <div class="player__body">
        <!-- Cover Section -->
        <div class="body__cover">
          <ul class="list list--cover">
            <div>
              <!-- Burger Icon -->
              <n-button text @click="toggleMenu" class="burger-button">
                <n-icon>
                  <template #default>
                    <menu-outlined />
                    
                  </template>
                  
                </n-icon>
              </n-button>

              <!-- Drawer for the Burger Menu -->
              <n-drawer v-model:show="isMenuOpen" placement="left" width="260px" closable>
                <n-menu
                  :options="menuOptions"
                  :default-value="selectedMenu"
                  @update:value="onMenuSelect"
                />
              </n-drawer>
            </div>

            <li>
              <a class="list__link" href="#"><i class="fa fa-search"></i></a>
            </li>
          </ul>
          <img src="./components/images/maxresdefault.jpg" alt="Album cover" class="album-cover" />
        </div>

        <!-- Song Info -->
        <div class="body__info">
          <div class="info__album">Entre dos tierras</div>
          <div class="info__song">Entre dos tierras</div>
          <div class="info__artist">Till Lindemann</div>
        </div>

        <!-- Controls -->
        <div class="body__buttons">
          <ul class="list list--buttons">
            <li>
              <a href="#" class="list__link"><i class="fa fa-step-backward"></i></a>
            </li>
            <li>
              <a href="#" class="list__link"><i class="fa fa-play"></i></a>
            </li>
            <li>
              <a href="#" class="list__link"><i class="fa fa-step-forward"></i></a>
            </li>
          </ul>
        </div>
      </div>

      <!-- Footer -->
      <div class="player__footer">
        <ul class="list list--footer">
          <li>
            <a href="#" class="list__link"><i class="fa fa-heart-o"></i></a>
          </li>
          <li>
            <a href="#" class="list__link"><i class="fa fa-random"></i></a>
          </li>
          <li>
            <a href="#" class="list__link"><i class="fa fa-undo"></i></a>
          </li>
          <li>
            <a href="#" class="list__link"><i class="fa fa-ellipsis-h"></i></a>
          </li>
        </ul>
      </div>
    </div>
    <a :href="authUrl" class="spotify-login-button">Login with Spotify</a>
  </div>

  <!-- Spotify Login -->
</template>

<style scoped lang="scss">
.burger-button {
  margin-top: 5px;
  font-size: 25px; /* Icon size */
  padding-left: 10px;
  // border: none;
  // background-color: transparent;
  cursor: pointer;
  color: white;
}
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

// Variables
$boxshadow-0: 0 1px 3px -5px rgba(0, 0, 0, 0.13), 0 1px 3px -10px rgba(0, 0, 0, 0.23);
$boxshadow-1: 0 3px 6px -5px rgba(0, 0, 0, 0.16), 0 3px 6px -10px rgba(0, 0, 0, 0.23);
$boxshadow-2: 0 10px 20px -5px rgba(0, 0, 0, 0.19), 0 6px 6px -10px rgba(0, 0, 0, 0.23);
$boxshadow-3: 0 14px 28px -5px rgba(0, 0, 0, 0.25), 0 10px 10px -10px rgba(0, 0, 0, 0.22);
$radius: remy(4px);

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

.body__cover {
  position: relative;
}

.body__cover img {
  max-width: 100%;
}

.list {
  display: flex;
  margin: 0;
  padding: 0;
  list-style-type: none;
}

.body__buttons,
.body__info,
.player__footer {
  padding-right: 2rem;
  padding-left: 2rem;
}

.list--cover,
.list--footer {
  justify-content: space-between;
}

.list--header .list__link,
.list--footer .list__link {
  color: #888;
}

.list--cover {
  position: absolute;
  top: 0.5rem;
  width: 100%;

  li:first-of-type {
    margin-left: 0.75rem;
  }

  li:last-of-type {
    margin-right: 0.75rem;
  }

  a {
    font-size: 1.15rem;
    color: #fff;
  }
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

.album-cover {
  width: 320px;
  height: 320px;
}

.body__info {
  padding-top: 1.5rem;
  padding-bottom: 1.25rem;
  text-align: center;
}

.info__album,
.info__song {
  margin-bottom: 0.5rem;
}

.info__artist,
.info__album {
  font-size: 0.75rem;
  font-weight: 300;
  color: #666;
}

.info__song {
  font-size: 1.15rem;
  font-weight: 400;
  color: $color-red;
}

.body__buttons {
  padding-bottom: 2rem;
}

.body__buttons {
  padding-top: 1rem;
}

.list--buttons {
  align-items: center;
  justify-content: center;
}

.list--buttons li:nth-of-type(n + 2) {
  margin-left: 1.25rem;
}

.list--buttons a {
  padding-top: 0.45rem;
  padding-right: 0.75rem;
  padding-bottom: 0.45rem;
  padding-left: 0.75rem;
  font-size: 1rem;
  border-radius: 50%;
  box-shadow: 0 3px 6px rgba(33, 33, 33, 0.1), 0 3px 12px rgba(33, 33, 33, 0.15);

  &:focus,
  &:hover {
    color: darken(rgba($color-red, 0.95), 8%);
    opacity: 1;
    box-shadow: 0 6px 9px rgba(33, 33, 33, 0.1), 0 6px 16px rgba(33, 33, 33, 0.15);
  }
}

.list--buttons li:nth-of-type(2) a {
  padding-top: 0.82rem;
  padding-right: 1rem;
  padding-bottom: 0.82rem;
  padding-left: 1.19rem;
  margin-left: 0.5rem;
  font-size: 1.25rem;
  color: rgba($color-red, 0.95);
}

.list--buttons li:first-of-type a,
.list--buttons li:last-of-type a {
  font-size: 0.95rem;
  color: #212121;
  opacity: 0.5;

  &:focus,
  &:hover {
    color: $color-red;
    opacity: 0.75;
  }
}

.list__link {
  @include transition;

  &:focus,
  &:hover {
    color: $color-red;
  }
}

.player__footer {
  padding-top: 1rem;
  padding-bottom: 2rem;
}

.list--footer a {
  opacity: 0.5;

  &:focus,
  &:hover {
    opacity: 0.9;
  }
}

.spotify-login-button {
  display: flex;
  // display: inline-block;
  text-align: center;
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #1db954;
  color: white;
  text-decoration: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: bold;
  transition: background-color 0.3s;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

.spotify-login-button:hover {
  background-color: #1ed760;
}
</style>
