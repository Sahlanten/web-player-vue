<script setup>
const clientId = "3a125a5c879d4e6f9eb662422e6548e8";
const redirectUri = "http://localhost:5173/callback";
const scopes = "user-read-playback-state user-modify-playback-state user-read-currently-playing";

const authUrl = `https://accounts.spotify.com/authorize?client_id=${clientId}&response_type=token&redirect_uri=${encodeURIComponent(
  redirectUri
)}&scope=${encodeURIComponent(scopes)}`;
</script>

<template>
  <a :href="authUrl" class="spotify-login-button">Login with Spotify</a>
</template>

<style lang="scss" scoped>
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
  cursor: pointer;
}
</style>
