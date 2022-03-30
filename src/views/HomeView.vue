<template>
  <div class="home">
    <button class="btn" @click="toggleModal">Open Modal bottom sheet</button>
      <transition name="fade">
        <div v-show="modalActive" class="overlay" @click="toggleModal">
          <ModalBottom @close="toggleModal" :modalActive="modalActive"/>
        </div>
      </transition>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import ModalBottom from '@/components/ModalBottom.vue'

export default defineComponent({
  components: {
    ModalBottom
  },
  setup () {
    const modalActive = ref(false)

    const toggleModal = () => {
      modalActive.value = !modalActive.value
      modalActive.value
        ? localStorage.setItem('modalActive', JSON.stringify(modalActive.value))
        : localStorage.removeItem('modalActive')
    }
    const setModalState = () => {
      const modalActive = localStorage.getItem('modalActive')
      if (modalActive) {
        toggleModal()
      }
    }

    return { modalActive, toggleModal, setModalState }
  },
  mounted () {
    this.setModalState()
  }
})
</script>

<style lang="scss" scoped>
.home {
  display: flex;
  justify-content: center;
  padding: 20px;
}
.overlay {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  height: 100vh;
  width: 100vw;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.4);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
