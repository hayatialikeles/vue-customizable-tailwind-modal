<template>
  <div id="app">
    <button :class="toggleBtnClass" @click="() => openModal()">
      <slot name="open-btn-slot"> Open Modal </slot>
    </button>

    <Transition name="fade">
      <div
        class="modal-overlay h-screen flex items-center justify-center w-full fixed top-0 bottom-0 left-0 right-0 bg-black bg-opacity-30"
        style="z-index: 99 !important"
        v-if="show"
        @click="closeModal()"
      >
        <div
          :class="containerClass"
          @mouseover="() => (isModalOver = true)"
          @mouseleave="() => (isModalOver = false)"
          style="z-index: 999 !important"
        >
          <slot name="header">
            <div :class="headerContainerClass">
              <h5>{{ title }}</h5>
              <button @click="closeModal(true)" :class="closeBtnClass">X</button>
            </div>
          </slot>
          <div :class="bodyContainerClass">
            <slot>body content </slot>
          </div>

          <footer :class="footerClass">
            <slot name="footer"> </slot>
          </footer>
        </div>
      </div>
    </Transition>
  </div>
</template>

<script>
export default {
  name: "App",
  props: {
    toggleBtnClass: {
      default: "w-full rounded p-2",
    },
    containerClass: {
      default: "w-6/12  shadow h-80 bg-gray-200 relative rounded",
    },
    title: {
      default: "Modal Title",
    },
    headerContainerClass: {
      default:
        "flex justify-between card-header p-4 border-b border-opacity-50 border-black",
    },
    closeBtnClass: {
      default: "w-6 h-6 text-black",
    },
    bodyContainerClass: {
      default: "p-4",
    },
    footerClass: {
      default: "",
    },
  },
  data() {
    return {
      show: false,
      isModalOver: false,
    };
  },
  methods: {
    openModal() {
      this.show = true;
      this.$emit("opened", true);
    },
    closeModal(closeBtn) {
      if (!this.isModalOver || closeBtn) {
        this.show = false;
        this.$emit("closed", true);
      }
    },
  },
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
