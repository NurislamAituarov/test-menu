<template>
  <header class="header">
    <div class="container">
      <div class="header__info">
        <div class="logo">
          <img src="/Logo.svg" alt="logo" />
        </div>

        <div class="wrapper__notification">
          <p class="map">Москва и область</p>
          <div
            class="notification"
            @click="() => (toggleAnimation = !toggleAnimation)"
            :class="{ 'toggle-animation': toggleAnimation }"
          >
            <img class="bell" src="/Notification-Bell.svg" alt="Notification" />
            <img
              v-if="!toggleAnimation"
              class="indicator"
              src="/inbox_indicator.svg"
              alt="Indicator"
            />
          </div>

          <MenuHamburger />
        </div>
      </div>
      <TheNav />
    </div>
  </header>
</template>

<script setup>
import { ref } from "vue";
import TheNav from "./TheNav.vue";
import MenuHamburger from "./MenuHamburger.vue";
const toggleAnimation = ref(false);
</script>

<style lang="scss">
.header {
  border-bottom: 1px solid #d3d9df;
  overflow-x: hidden;
}

.header__info {
  background-color: #1f2229;
  padding: 6px 0 8px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;

  &::after {
    content: "";
    position: absolute;
    top: 0;
    right: -100%;
    width: 100%;
    height: 100%;
    background-color: inherit;
  }
  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background-color: inherit;
  }
}

.wrapper__notification {
  display: flex;
  align-items: center;
  gap: 32px;

  .notification {
    position: relative;
    height: 25px;
    animation: bell 1s 1s both infinite;
    cursor: pointer;
    .bell {
      transform: rotate(30deg);
    }

    .indicator {
      position: absolute;
      top: 3px;
      right: 4px;
    }
  }

  .toggle-animation {
    animation: toggle;
  }
}

@keyframes bell {
  0% {
    transform: rotate(0deg);
  }
  10% {
    transform: rotate(30deg);
  }
  20% {
    transform: rotate(0);
  }
  80% {
    transform: rotate(0);
  }
  90% {
    transform: rotate(-30deg);
  }
  100% {
    transform: rotate(0);
  }
}

@media screen and (max-width: 768px) {
  .header__info {
    padding: 13px 0 14px;
  }

  .map {
    display: none;
  }
  .wrapper__notification {
    gap: 8px;
  }
}
</style>