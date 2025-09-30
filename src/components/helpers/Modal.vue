<template>
  <transition name="modal-fade">
    <div class="modal-backdrop" @click="$emit('close')">
      <div class="modal" :class="{ 'night-mode': nightMode }" @click.stop>
        <header class="modal-header">
          <h5 class="modal-title">{{ portfolio.name }}</h5>
          <button type="button" class="btn-close" @click="$emit('close')"></button>
        </header>
        <section class="modal-body">
          <div class="mb-2 text-muted small">
            <span>{{ portfolio.date }} • {{ portfolio.category }}</span>
          </div>
          <div class="mb-3">
            <span v-for="tech in portfolio.technologies" :key="tech" class="badge me-2 mb-2">{{ tech }}</span>
          </div>
          <p v-html="portfolio.description"></p>
          <Gallery :images="portfolio.pictures" />
        </section>
        <footer class="modal-footer">
          <a :href="portfolio.github" target="_blank" class="btn btn-outline-primary">GitHub</a>
          <a v-if="portfolio.visit" :href="portfolio.visit" target="_blank" class="btn btn-primary">Visit Website</a>
          <button type="button" class="btn btn-secondary" @click="$emit('close')">Close</button>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
import Gallery from "./Gallery.vue";

export default {
  name: "Modal",
  components: {
    Gallery,
  },
  props: {
    portfolio: Object,
    nightMode: Boolean,
  },
};
</script>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1050;
}

.modal {
  background-color: var(--surface-color);
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  width: 80%;
  max-width: 800px;
  max-height: 90vh;
  display: flex;
  flex-direction: column;
}

.modal-header,
.modal-footer {
  padding: 1rem;
  border-bottom: 1px solid #dee2e6;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal-footer {
  border-top: 1px solid #dee2e6;
  border-bottom: none;
}

.night-mode .modal-header, .night-mode .modal-footer {
    border-color: #4d4d4d;
}

.modal-title {
  color: var(--heading-color);
  font-weight: 700;
}

.modal-body {
  padding: 1rem;
  overflow-y: auto;
  color: var(--text-color);
}

.btn-close {
  background: none;
  border: none;
  font-size: 1.5rem;
  color: var(--text-color);
}

.night-mode .btn-close {
    filter: invert(1) grayscale(100%) brightness(200%);
}

.badge {
  background-color: var(--primary-color);
  color: var(--surface-color);
}

.night-mode .badge {
    background-color: var(--secondary-color);
    color: #000;
}

.modal-fade-enter-active, .modal-fade-leave-active {
  transition: opacity 0.3s;
}
.modal-fade-enter, .modal-fade-leave-to {
  opacity: 0;
}
</style>