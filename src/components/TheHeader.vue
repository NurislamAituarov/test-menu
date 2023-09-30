<template>
  <header class="header">
    <div class="container">
      <div class="header__info">
        <div class="logo">
          <img src="/Logo.svg" alt="logo" />
        </div>

        <div class="wrapper__notification">
          <p class="location">
            <img src="/location.svg" alt="Location" />
            Москва и область
          </p>
          <THeNotification
            :toggleAnimation="toggleAnimation"
            @on-active-animation="onActiveAnimation"
          />
          <MenuHamburger @on-active-menu="onActiveMenu" />
        </div>
      </div>
      <TheNav v-if="activeMenu || width > 768" />
    </div>
  </header>
  <p v-if="activeMenu" class="location-mobile">
    <img src="/location.svg" alt="Location" /> Москва и область
  </p>
</template>

<script setup>
import { onMounted, ref } from "vue";
import TheNav from "./TheNav.vue";
import MenuHamburger from "./MenuHamburger.vue";
import THeNotification from "./THeNotification.vue";
const toggleAnimation = ref(false);
const activeMenu = ref(false);
const width = ref();

onMounted(() => {
  const onResize = () => (width.value = window.innerWidth);
  onResize();
  window.addEventListener("resize", onResize);
});

function onActiveMenu() {
  activeMenu.value = !activeMenu.value;
}
function onActiveAnimation() {
  toggleAnimation.value = !toggleAnimation.value;
}
</script>

<style lang="scss">
.header {
  border-bottom: 1px solid #d3d9df;
  overflow-x: hidden;
}

.header__info {
  background-color: #1f2229;
  padding: 9px 0 10px;
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
.location {
  display: flex;
  align-items: center;
  gap: 13px;
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
.location-mobile {
  display: none;
  animation: location-anim 0.5s both;
}

@media screen and (max-width: 768px) {
  .header {
    border: none;
    flex: 1;
  }
  .header__info {
    padding: 13px 0 14px;
  }

  .location {
    display: none;
  }
  .wrapper__notification {
    gap: 8px;
  }

  .location-mobile {
    display: flex;
    align-items: center;
    gap: 8px;
    background-color: #f3f5f6;
    min-height: 56px;
    padding: 16px;
    font-size: 16px;
    line-height: 22px;
  }
}
</style>