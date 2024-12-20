<script setup></script>

<template>
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
</template>

<style lang="scss" scoped>
// Functions
@function remy($value, $base: 16px) {
  @return ($value / $base) * 1rem;
}

// Mixins
@mixin transition($prop: all, $duration: 0.25s, $timing: cubic-bezier(0.4, 0, 1, 1)) {
  transition: $prop $duration $timing;
}

$color-red: #d30320;    

.body__buttons {
  padding: 2rem;
}

.list__link {
  color: #888;
  @include transition;

  &:focus,
  &:hover {
    color: $color-red;
  }
}

.list {
  display: flex;
  margin: 0;
  padding: 0;
  list-style-type: none;
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
</style>
