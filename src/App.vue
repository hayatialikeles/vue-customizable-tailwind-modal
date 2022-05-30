<template>
  <div id="app">
    <button :class="toggleBtnClass" @click="() => openModal()">
      <slot name="open-btn-slot"> Open Modal </slot>
    </button>

    <Transition name="fade">
      <div
        class="modal-overlay flex items-center justify-center overflow-y-auto fixed inset-0 bg-black bg-opacity-30 dark:bg-gray-500 dark:bg-opacity-40"
        style="z-index: 99 !important"
        v-if="show"
        @click="closeModal()"
      >
        <div
          :class="containerClass"
          @mouseover="() => (isModalOver = true)"
          @mouseleave="() => (isModalOver = false)"
          style="z-index: 999 !important"
          role="dialog"
          aria-labelledby="modalTitle"
          aria-describedby="modalDescription"
        >
          <slot name="header">
            <div :class="headerContainerClass" id="modalTitle">
              <h5>{{ title }}</h5>
              <button @click="closeModal(true)" :class="closeBtnClass">X</button>
            </div>
          </slot>

          <div :class="bodyContainerClass" id="modalDescription">
            <div v-if="isLoad" class="p-6 text-center">
              <i class="fas fa-spinner fa-spin fa-3x"></i>
            </div>
            <slot v-if="!isLoad">body content </slot>
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
    isLoad: {
      type: Boolean,
      default: false,
    },
    toggleBtnClass: {
      default: "w-full rounded p-2",
    },
    containerClass: {
      default:
        "w-full md:w-6/12 bg-white h-full md:h-auto  md:overflay-y-auto pt-0 mt-44 mb-4 dark:bg-gray-800 rounded",
    },
    title: {
      default: "Modal Title",
    },
    headerContainerClass: {
      default:
        "flex justify-between card-header p-4 border-b border-opacity-50 border-black  bg-white w-full dark:bg-gray-900 dark:text-gray-300 rounded-t",
    },

    closeBtnClass: {
      default: "w-6 h-6 text-black dark:text-gray-300",
    },
    bodyContainerClass: {
      default: "h-auto py-4 px-4 ",
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
