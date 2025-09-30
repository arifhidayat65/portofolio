<template>
  <div class="card h-100" :class="{ 'night-mode': nightMode }">
    <img :src="portfolio.pictures[0].img" class="card-img-top" alt="Portfolio Image">
    <div class="card-body d-flex flex-column">
      <h5 class="card-title fw-bold">{{ portfolio.name }}</h5>
      <div class="d-flex flex-wrap mb-2">
          <span v-for="tech in portfolio.technologies" :key="tech" class="badge me-2 mb-2">{{ tech }}</span>
      </div>
      <p class="card-text flex-grow-1">{{ portfolio.description }}</p>
      <div class="mt-auto text-center">
        <a v-if="portfolio.visit" :href="portfolio.visit" target="_blank" class="btn btn-sm btn-outline-primary">Visit Website</a>
        <button @click="$emit('show', portfolio)" class="btn btn-sm btn-primary ms-2">Details</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    portfolio: {
      type: Object,
    },
    nightMode: {
      type: Boolean,
    },
  },
};
</script>

<style scoped>
.card {
  background-color: var(--surface-color);
  border: none;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  transition: transform 0.3s, box-shadow 0.3s;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 30px rgba(0,0,0,0.15);
}

.card-img-top {
  height: 200px;
  object-fit: cover;
  border-top-left-radius: var(--border-radius);
  border-top-right-radius: var(--border-radius);
}

.card-body {
  color: var(--text-color);
}

.card-title {
    color: var(--heading-color);
}

.badge {
  background-color: var(--primary-color);
  color: var(--surface-color);
}

.night-mode .badge {
    background-color: var(--secondary-color);
    color: #000;
}

.btn-primary {
    background-color: var(--primary-color);
    border-color: var(--primary-color);
    color: var(--surface-color);
}

.btn-primary:hover {
    background-color: #2980b9;
    border-color: #2980b9;
}

.night-mode .btn-primary:hover {
    background-color: #9a65d9;
    border-color: #9a65d9;
}

.btn-outline-primary {
    color: var(--primary-color);
    border-color: var(--primary-color);
}

.btn-outline-primary:hover {
    background-color: var(--primary-color);
    color: var(--surface-color);
}
</style>