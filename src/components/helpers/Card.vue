<template>
  <div class="card h-100" :class="{ 'light-mode': !nightMode }">
    <div class="card-img-wrap">
      <img :src="portfolio.pictures[0].img" class="card-img-top" :alt="portfolio.name">
    </div>
    <div class="card-body d-flex flex-column">
      <h5 class="card-title">{{ portfolio.name }}</h5>
      <div class="card-tags mb-3">
        <span class="card-tag mono" v-for="tech in portfolio.technologies" :key="tech">{{ tech }}</span>
      </div>
      <p class="card-text flex-grow-1">{{ portfolio.description }}</p>
      <div class="mt-auto d-flex gap-2 justify-content-center">
        <a
          v-if="portfolio.visit"
          :href="portfolio.visit"
          target="_blank"
          rel="noopener"
          class="btn-outline"
          aria-label="Visit website"
        >Visit</a>
        <button
          @click="$emit('show', portfolio)"
          class="btn-primary"
          aria-label="View details"
        >Details</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    portfolio: { type: Object },
    nightMode: { type: Boolean },
  },
};
</script>

<style scoped>
.card {
  background-color: var(--color-card);
  border: 1px solid var(--color-border);
  border-radius: var(--border-radius);
  box-shadow: 0 4px 20px rgba(0,0,0,0.3);
  transition: transform 0.25s ease, box-shadow 0.25s ease, border-color 0.25s ease;
  overflow: hidden;
}

.card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 40px rgba(0,0,0,0.4);
  border-color: rgba(34, 197, 94, 0.3);
}

.card.light-mode {
  background-color: #FFFFFF;
  border-color: #E2E8F0;
  box-shadow: 0 2px 12px rgba(0,0,0,0.06);
}
.card.light-mode:hover {
  box-shadow: 0 8px 24px rgba(0,0,0,0.1);
  border-color: rgba(22, 163, 74, 0.3);
}

.card-img-wrap { overflow: hidden; }

.card-img-top {
  width: 100%;
  height: 200px;
  object-fit: cover;
  transition: transform 0.35s ease;
}

.card:hover .card-img-top { transform: scale(1.04); }

.card-body {
  padding: 20px;
  color: var(--color-foreground);
}
.card.light-mode .card-body { color: #0F172A; }

.card-title {
  font-size: 1rem;
  font-weight: 600;
  color: var(--color-foreground);
  margin-bottom: 10px;
}
.card.light-mode .card-title { color: #0F172A; }

.card-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}

.card-tag {
  font-size: 0.68rem;
  background-color: var(--color-muted);
  color: var(--color-muted-fg);
  border: 1px solid var(--color-border);
  padding: 2px 7px;
  border-radius: 4px;
  white-space: nowrap;
}
.card.light-mode .card-tag {
  background: #F1F5F9;
  color: #475569;
  border-color: #CBD5E1;
}

.card-text {
  font-size: 0.85rem;
  color: var(--color-muted-fg);
  line-height: 1.6;
  margin-bottom: 16px;
}
.card.light-mode .card-text { color: #64748B; }

/* Buttons */
.btn-primary, .btn-outline {
  font-family: "IBM Plex Sans", sans-serif;
  font-weight: 500;
  font-size: 0.82rem;
  padding: 7px 18px;
  border-radius: 7px;
  cursor: pointer;
  transition: background-color 0.2s ease, color 0.2s ease, transform 0.2s ease;
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  outline: none;
}

.btn-primary {
  background-color: var(--color-accent);
  color: var(--color-on-accent);
  border: none;
}
.btn-primary:hover {
  background-color: #16A34A;
  transform: translateY(-1px);
}

.btn-outline {
  background: transparent;
  border: 1px solid var(--color-border);
  color: var(--color-muted-fg);
}
.btn-outline:hover {
  border-color: var(--color-accent);
  color: var(--color-accent);
}

.btn-primary:focus-visible, .btn-outline:focus-visible {
  outline: 2px solid var(--color-ring);
  outline-offset: 2px;
}

.card.light-mode .btn-primary { background-color: #16A34A; color: #FFFFFF; }
.card.light-mode .btn-primary:hover { background-color: #15803D; }
.card.light-mode .btn-outline { border-color: #CBD5E1; color: #475569; }
.card.light-mode .btn-outline:hover { border-color: #16A34A; color: #16A34A; }
</style>
