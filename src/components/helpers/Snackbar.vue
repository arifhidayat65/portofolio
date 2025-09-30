<template>
  <transition name="snackbar-fade">
    <div v-if="showSnackbar" class="snackbar" :style="{ backgroundColor: snackbarColor }">
      {{ snackbarMessage }}
    </div>
  </transition>
</template>

<script>
export default {
  name: "Snackbar",
  props: {
    showSnackbar: Boolean,
    snackbarMessage: String,
    snackbarColor: String,
  },
  watch: {
    showSnackbar(newValue) {
      if (newValue) {
        setTimeout(() => {
          this.$emit("close", false);
        }, 3000);
      }
    },
  },
};
</script>

<style scoped>
.snackbar {
  position: fixed;
  bottom: 20px;
  right: 20px;
  padding: 15px 25px;
  border-radius: var(--border-radius);
  color: white;
  font-weight: 500;
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
  z-index: 1051;
}

.snackbar-fade-enter-active, .snackbar-fade-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}
.snackbar-fade-enter, .snackbar-fade-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
</style>