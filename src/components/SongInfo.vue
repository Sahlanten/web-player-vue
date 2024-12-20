<script setup></script>

<template>
  <div class="body__info">
    <div class="info__album">Entre dos tierras</div>
    <div class="info__song">Entre dos tierras</div>
    <div class="info__artist">Till Lindemann</div>
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

$color-red: #d30320;

.body__info {
  padding-right: 2rem;
  padding-left: 2rem;
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
</style>
