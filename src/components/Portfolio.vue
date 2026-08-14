<template>
  <div class="section portfolio-section" :class="{ 'light-mode': !nightMode }">
    <div class="container">
      <div class="section-header text-center mb-5" data-aos="fade-down" data-aos-duration="700">
        <span class="section-label mono">// portfolio</span>
        <h2 class="section-title">My Work</h2>
        <div class="title-line"></div>
      </div>

      <!-- Tab switcher -->
      <div class="tab-switcher text-center mb-5">
        <button
          class="tab-btn"
          :class="{ active: activeTab === 'development' }"
          @click="activeTab = 'development'"
        >Development</button>
        <button
          class="tab-btn"
          :class="{ active: activeTab === 'design' }"
          @click="activeTab = 'design'"
        >Design</button>
      </div>

      <!-- Development cards -->
      <div v-if="activeTab === 'development'">
        <div class="row g-4">
          <div
            class="col-lg-4 col-md-6"
            v-for="(portfolio, index) in displayedPortfolios"
            :key="index"
            data-aos="fade-up"
            :data-aos-delay="index * 80"
          >
            <Card :portfolio="portfolio" :nightMode="nightMode" @show="showModalFn" />
          </div>
        </div>
        <div class="text-center mt-5" v-if="all_info.length > displayedPortfolios.length">
          <button class="load-more-btn" @click="loadMore">Load More</button>
        </div>
      </div>

      <!-- Design cards -->
      <div v-if="activeTab === 'design'">
        <div class="row g-4">
          <div
            class="col-lg-4 col-md-6"
            v-for="(design, index) in design_info"
            :key="index"
            data-aos="fade-up"
            :data-aos-delay="index * 80"
          >
            <Card :portfolio="design" :nightMode="nightMode" @show="showDesignModalFn" />
          </div>
        </div>
      </div>
    </div>

    <Modal v-if="showModal" :portfolio="modal_info" :nightMode="nightMode" @close="closeModal" />
    <DesignModal v-if="showDesignModal" :portfolio="design_modal_info" :nightMode="nightMode" @close="closeModal" />
  </div>
</template>

<script>
import Card from "./helpers/Card.vue";
import Modal from "./helpers/Modal.vue";
import DesignModal from "./helpers/DesignModal.vue";
import info from "../../info";

export default {
  name: "Portfolio",
  components: { Card, Modal, DesignModal },
  props: {
    nightMode: { type: Boolean },
  },
  data() {
    return {
      activeTab: "development",
      all_info: info.portfolio,
      design_info: info.portfolio_design,
      displayedPortfolios: [],
      showModal: false,
      showDesignModal: false,
      modal_info: {},
      design_modal_info: {},
      itemsPerLoad: 6,
    };
  },
  created() {
    this.loadMore();
  },
  methods: {
    loadMore() {
      const current = this.displayedPortfolios.length;
      this.displayedPortfolios.push(...this.all_info.slice(current, current + this.itemsPerLoad));
    },
    showModalFn(p) { this.modal_info = p; this.showModal = true; },
    showDesignModalFn(d) { this.design_modal_info = d; this.showDesignModal = true; },
    closeModal() { this.showModal = false; this.showDesignModal = false; },
  },
};
</script>

<style scoped>
.section {
  background-color: var(--color-background);
  padding: 80px 0;
}
.section.light-mode { background-color: #F8FAFC; }

.section-label {
  font-size: 0.8rem;
  color: var(--color-accent);
  display: block;
  margin-bottom: 8px;
  letter-spacing: 0.06em;
}
.section.light-mode .section-label { color: #16A34A; }

.section-title {
  font-size: clamp(1.6rem, 3vw, 2.2rem);
  font-weight: 700;
  color: var(--color-foreground);
  margin-bottom: 12px;
}
.section.light-mode .section-title { color: #0F172A; }

.title-line {
  width: 48px;
  height: 3px;
  background: var(--color-accent);
  border-radius: 2px;
  margin: 0 auto;
  box-shadow: 0 0 8px rgba(34, 197, 94, 0.4);
}
.section.light-mode .title-line { box-shadow: none; }

/* Tab switcher */
.tab-switcher {
  display: flex;
  gap: 8px;
  justify-content: center;
}

.tab-btn {
  background: var(--color-muted);
  border: 1px solid var(--color-border);
  color: var(--color-muted-fg);
  font-family: "IBM Plex Sans", sans-serif;
  font-weight: 500;
  font-size: 0.9rem;
  padding: 8px 24px;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s ease, color 0.2s ease, border-color 0.2s ease;
  outline: none;
}

.tab-btn:hover {
  color: var(--color-foreground);
  border-color: var(--color-border);
  background-color: var(--color-secondary);
}

.tab-btn.active {
  background-color: var(--color-accent);
  color: var(--color-on-accent);
  border-color: var(--color-accent);
  font-weight: 600;
}

.tab-btn:focus-visible {
  outline: 2px solid var(--color-ring);
  outline-offset: 2px;
}

.section.light-mode .tab-btn {
  background: #FFFFFF;
  border-color: #CBD5E1;
  color: #475569;
}
.section.light-mode .tab-btn:hover {
  background: #F1F5F9;
  color: #0F172A;
}
.section.light-mode .tab-btn.active {
  background-color: #16A34A;
  color: #FFFFFF;
  border-color: #16A34A;
}

/* Load more */
.load-more-btn {
  background: transparent;
  border: 1px solid var(--color-accent);
  color: var(--color-accent);
  font-family: "IBM Plex Sans", sans-serif;
  font-weight: 500;
  padding: 10px 28px;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s ease, color 0.2s ease;
  outline: none;
}

.load-more-btn:hover {
  background-color: var(--color-accent);
  color: var(--color-on-accent);
}

.load-more-btn:focus-visible {
  outline: 2px solid var(--color-ring);
  outline-offset: 2px;
}

.section.light-mode .load-more-btn {
  border-color: #16A34A;
  color: #16A34A;
}
.section.light-mode .load-more-btn:hover {
  background-color: #16A34A;
  color: #FFFFFF;
}
</style>
