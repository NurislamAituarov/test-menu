<template>
  <div
    class="notification"
    @click="$emit('on-active-animation')"
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
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

defineProps({
  toggleAnimation: { type: Boolean, default: false },
});

defineEmits(["on-active-animation"]);
</script>