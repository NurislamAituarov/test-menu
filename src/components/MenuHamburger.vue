<template>
  <div class="menu-hamburger">
    <input
      ref="refMenu"
      type="checkbox"
      id="checkbox1"
      className="checkbox1 visuallyHidden"
    />
    <label htmlFor="checkbox1">
      <div @click="showMenu" className="hamburger hamburger1">
        <span className="bar bar1"></span>
        <span className="bar bar2"></span>
        <span className="bar bar3"></span>
        <span className="bar bar4"></span>
      </div>
    </label>
  </div>
</template>


<script setup>
import { ref, defineEmits } from "vue";

const emit = defineEmits(["on-active-menu"]);

const refMenu = ref();
const activeMenu = ref(false);

function showMenu() {
  refMenu.value?.checked
    ? (activeMenu.value = true)
    : (activeMenu.value = false);
  emit("on-active-menu");
}
</script>

<style scoped lang="scss">
.menu-hamburger {
  display: none;
}
.visuallyHidden {
  display: none;
}
.hamburger {
  margin: 0 auto;
  width: 18px;
  height: 14px;
  position: relative;
  cursor: pointer;
}

.hamburger .bar {
  padding: 0;
  width: 18px;
  height: 2px;
  background-color: white;
  display: block;
  border-radius: 4px;
  transition: all 0.4s ease-in-out;
  position: absolute;
}

.bar1 {
  top: 0;
}

.bar2,
.bar3 {
  top: 6px;
}

.bar3 {
  right: 0;
}

.bar4 {
  bottom: 0;
}

/* HAMBURGER 1 */
.checkbox1:checked + label > .hamburger1 > .bar1 {
  transform: rotate(45deg);
  transform-origin: 0%;
  width: 18px;
}

.checkbox1:checked + label > .hamburger1 > .bar2 {
  transform: translateX(-40px);
  background-color: transparent;
}

.checkbox1:checked + label > .hamburger1 > .bar3 {
  transform: translateX(40px);
  background-color: transparent;
}

.checkbox1:checked + label > .hamburger1 > .bar4 {
  transform-origin: 8%;
  transform: rotate(-45deg);
  width: 18px;
}

@media screen and (max-width: 768px) {
  .menu-hamburger {
    display: block;
  }
}
</style>