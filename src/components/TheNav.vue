<template>
  <nav class="nav">
    <ul>
      <li tabindex="0" v-for="list of navList" :key="list.id">
        {{ list.name }}
      </li>
    </ul>
  </nav>
</template>

<script setup>
import { useStore } from "vuex";

const store = useStore();
const navList = store.state.nav;
</script>

<style lang="scss">
.nav {
  height: 47px;
  padding: 17px 0;

  ul {
    display: flex;
    align-items: center;
    gap: 18px;
    li {
      position: relative;
      cursor: pointer;
      transition: 0.3s;
      font-size: 14px;
      line-height: 18px;
      overflow: hidden;
      padding-bottom: 12px;

      &::before {
        content: "";
        position: absolute;
        width: 100%;
        height: 2px;
        bottom: 0;
        left: -100%;
        background-color: #1f2229;
        transition: 0.3s;
      }
      &:hover,
      &:focus {
        color: #1f2229;
        &::before {
          left: 0;
        }
      }
    }
  }
}

@media (max-width: 822px) {
  .nav ul {
    gap: 10px;
  }
}

@media (max-width: 822px) {
  .nav {
    display: none;
  }
}
</style>