<script setup></script>

<template>
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

.player__footer {
  padding-top: 1rem;
  padding-bottom: 2rem;
}
.player__footer {
  padding-right: 2rem;
  padding-left: 2rem;
}

.list {
  display: flex;
  margin: 0;
  padding: 0;
  list-style-type: none;
}

.list--footer {
  color: #888;
  justify-content: space-between;
}
.list__link {
  color: #888;
  @include transition;

  &:focus,
  &:hover {
    color: $color-red;
  }
}
</style>
