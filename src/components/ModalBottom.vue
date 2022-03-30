<template>
  <transition name="slide">
    <div v-if="modalActive" class="modal" @click.stop>
      <div class="modal-content">
        <h2>Modal header</h2>
        <p> This is a modal message</p>
      </div>
      <button class="btn" @click="$emit('close')">Close</button>
    </div>
  </transition>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    modalActive: Boolean
  }
})
</script>

<style lang="scss" scoped>
.modal {
  position: relative;
  max-width: 100%;
  width: 100vw;
  background-color: #fff;
  padding: 20px;
  &-content {
    padding-bottom: 50px;
  }
}
.slide-enter-active {
  transition: all .3s cubic-bezier(0.52, 0.02, 0.19, 1.02) 0.15s;
}
.slide-leave-active {
  transition: all .3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}
.slide-enter-from {
  opacity: 0;
  transform: translateY(130px);
}
.slide-leave-to {
  transform: translateY(130px);
}
</style>
